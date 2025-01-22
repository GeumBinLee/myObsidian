---
created: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
updated: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
tags:
  - monthlynote
score:
---
<%*
const title = `${tp.date.now("YYYY년 M월")}`;
const daysInMonth = moment().daysInMonth();

let output = `# ${title}\n\n`;

output += "## GOALS\n";

// 주차별 목표를 동적으로 생성
for (let week = 1; week <= 5; week++) {
  const weeklyTitle = `${tp.date.now("YYYY년 M월")} ${week}주차`; // 각 주차별 제목 생성
  const tasksScript = `\`\`\`tasks
path includes LIFE/2025/WEEKLY NOTE/${weeklyTitle}
heading includes GOAL
\`\`\``;
  
  output += `### Week ${week} GOAL\n`;
  output += `${tasksScript}\n\n`;
}

output += "## DAYS OF THE MONTH\n";

// 월별 날짜 목록 생성
for (let day = 1; day <= daysInMonth; day++) {
  output += `- [<] ⏳ ${moment().startOf("month").add(day - 1, 'days').format("YYYY-MM-DD")}\n`;
}

// 최종 출력
tR = output;
%>



## MOOD AND SCORE TRACKER
```dataviewjs
// 현재 월의 시작과 다음 월의 시작 계산
const currentMonth = moment().startOf("month").format("YYYY-MM-DD");
const nextMonth = moment().startOf("month").add(1, "month").format("YYYY-MM-DD");

const pages = dv.pages('"LIFE/2025/DAILY NOTE"')
    .where(p => p.file.day >= dv.date(currentMonth) && p.file.day < dv.date(nextMonth));

let totalScore = 0;
let scoreCount = 0;

const rows = pages.map(p => {
    const date = p.file.link;
    const weather = p.weather ? p.weather.join(", ") : "-";
    const moods = p.moods ? p.moods.join(", ") : "-";
    const score = p.score !== undefined ? p.score : "-";

    // 점수 합계 및 개수 계산
    if (p.score !== undefined && typeof p.score === "number") {
        totalScore += p.score;
        scoreCount++;
    }

    return [date, weather, moods, score];
});

// 평균 점수 계산
const averageScore = scoreCount > 0 ? (totalScore / scoreCount).toFixed(2) : "-";

// Dataview 테이블 생성 (CSS 클래스 추가)
dv.table(
    ["날짜", "날씨", "기분", "점수"],
    [
        ...rows,
        // 분리선 행 추가 (CSS 클래스 사용)
        ["평균", "", "", averageScore]
    ],
    { cssClass: "dataview-custom-table" } // 커스텀 CSS 클래스 지정
);


```

## REVIEW
- [p] Good
- [b] Bad