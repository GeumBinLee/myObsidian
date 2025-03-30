---
created: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
updated: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
tags:
  - monthlynote
score:
---
<%*
const title = `${tp.date.now("YYYY-MM")}`;
const daysInMonth = moment().daysInMonth();
let output = `# ${tp.date.now("YYYY년 MM월")}
`;

output += "## GOALS\n";
output += "> [!note] 이번 달 목표\n> - [*] \n> - [*] \n> - [*] \n\n";

// 현재 월의 모든 주간 월요일 및 주차 계산 (weekly note와 동일한 방식 적용)
let firstDayOfMonth = moment().startOf("month");
let firstMonday = firstDayOfMonth.clone().startOf("isoWeek");
if (firstMonday.month() !== firstDayOfMonth.month()) {
    firstMonday.add(7, "days");
}

let weekCount = 0;
let currentMonday = firstMonday.clone();
const weeklyTitles = [];

while (currentMonday.month() === firstDayOfMonth.month() || currentMonday.clone().add(6, 'days').month() === firstDayOfMonth.month()) {
    // 주간 날짜별 개수를 계산하여 더 많은 일수가 포함된 달을 기준으로 설정
    const weekDays = Array.from({ length: 7 }, (_, i) => currentMonday.clone().add(i, 'days'));
    const monthCounts = {};
    weekDays.forEach(day => {
        const monthKey = `${day.year()}-${String(day.month() + 1).padStart(2, "0")}`;
        monthCounts[monthKey] = (monthCounts[monthKey] || 0) + 1;
    });
    const assignedMonth = Object.entries(monthCounts).reduce((a, b) => (b[1] > a[1] ? b : a))[0];
    const [assignedYear, assignedMonthNum] = assignedMonth.split('-').map(Number);
    
    // 해당 월의 첫 번째 월요일 찾기
    const monthStart = moment(`${assignedYear}-${String(assignedMonthNum).padStart(2, "0")}-01`).startOf('month');
    let assignedFirstMonday = monthStart.clone().startOf('isoWeek');
    if (assignedFirstMonday.month() + 1 !== assignedMonthNum) {
        assignedFirstMonday.add(7, 'days');
    }
    
    // 해당 월의 몇 번째 주인지 계산
    const weekIndexInMonth = currentMonday.diff(assignedFirstMonday, 'weeks') + 1;
    
    // 주차 제목 설정
    const weeklyTitle = `${assignedYear}-${String(assignedMonthNum).padStart(2, "0")}-W${String(weekIndexInMonth).padStart(2, "0")}`;
    weeklyTitles.push(weeklyTitle);
    currentMonday.add(7, "days");
}

// 주차별 목표 동적으로 생성 (weekly note의 주차와 일치)
weeklyTitles.forEach((weeklyTitle) => {
    output += `### [[${weeklyTitle}]] GOAL\n`;
    output += "- [*] \n\n";
});

output += "## DAYS OF THE MONTH\n> [!note]- What the icon means\n> - [<] 일정\n> - [>] 미뤄진 일정\n> - [!] 중요한 일정\n> - [l] 오프라인 약속\n> - [w] 기념일\n";

// 월별 날짜 목록 생성
for (let day = 1; day <= daysInMonth; day++) {
    output += `- [<] (${moment().startOf("month").add(day - 1, 'days').format("ddd")}) (@[[${moment().startOf("month").add(day - 1, 'days').format("YYYY-MM-DD")}]] 00:00PM) ⏳ ${moment().startOf("month").add(day - 1, 'days').format("YYYY-MM-DD")}\n`;
}

// 최종 출력
tR = output;

// 파일 이동
const destinationFolder = `LIFE/2025/MONTHLY NOTE`; // 이동할 폴더 경로
await tp.file.move(`${destinationFolder}/${title}`);
%>


## MOOD AND SCORE TRACKER
```dataviewjs
// 현재 파일 제목에서 월 정보 가져오기
const fileTitle = dv.current().file.name; // 예: "2025-02"
const currentMonth = moment(fileTitle, "YYYY-MM").startOf("month").format("YYYY-MM-DD");
const nextMonth = moment(fileTitle, "YYYY-MM").startOf("month").add(1, "month").format("YYYY-MM-DD");

// 해당 월의 노트 필터링
const pages = dv.pages('"LIFE/2025/DAILY NOTE"')
    .where(p => p.file.day >= dv.date(currentMonth) && p.file.day < dv.date(nextMonth))
    .sort(p => p.file.day, 'asc'); // 날짜를 오름차순으로 정렬

let totalScore = 0;
let scoreCount = 0;
let moodFrequency = {};
let weatherFrequency = {};

// 데이터 가공
const rows = pages.map(p => {
    const date = p.file.link;
    const weather = Array.isArray(p.weather) ? p.weather.join(", ") : (p.weather || "-");
    const moods = Array.isArray(p.moods) ? p.moods.join(", ") : (p.moods || "-");
    const score = p.score !== undefined ? p.score : "-";

    // 점수 합계 및 개수 계산
    if (p.score !== undefined && typeof p.score === "number") {
        totalScore += p.score;
        scoreCount++;
    }

    // 기분 빈도수 계산
    if (Array.isArray(p.moods)) {
        p.moods.forEach(mood => {
            moodFrequency[mood] = (moodFrequency[mood] || 0) + 1;
        });
    } else if (p.moods) {
        moodFrequency[p.moods] = (moodFrequency[p.moods] || 0) + 1;
    }
    
	// 날씨 빈도수 계산
	if (Array.isArray(p.weather)) {
	    p.weather.forEach(w => {
	        weatherFrequency[w] = (weatherFrequency[w] || 0) + 1;
	    });
	} else if (p.weather) {
	    weatherFrequency[p.weather] = (weatherFrequency[p.weather] || 0) + 1;
	}

    return [date, weather, moods, score];
});

// 평균 점수 계산
const averageScore = scoreCount > 0 ? (totalScore / scoreCount).toFixed(2) : "-";

// 가장 많이 나온 기분 찾기
const maxFrequency = Math.max(...Object.values(moodFrequency), 0);
const mostCommonMoods = Object.keys(moodFrequency).filter(mood => moodFrequency[mood] === maxFrequency).join(", ") || "-";

// 가장 많이 기록된 날씨 찾기 (기분과 동일한 방식)
const maxWeatherFrequency = Math.max(...Object.values(weatherFrequency), 0);
const mostCommonWeathers = Object.keys(weatherFrequency).filter(w => weatherFrequency[w] === maxWeatherFrequency).join(", ") || "-";

// Dataview 테이블 생성
dv.table(["날짜", "날씨", "기분", "점수"], [...rows, ["평균", mostCommonWeathers, mostCommonMoods, averageScore]]);
```

## REVIEW
- [p] Good
- [b] Bad