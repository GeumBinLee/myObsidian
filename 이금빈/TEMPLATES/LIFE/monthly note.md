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
let output = `# GOALS\n`;

output += "> [!note] 이번 달 목표\n> - [*] \n> - [*] \n> - [*] \n\n";

// 현재 월의 모든 ISO 주간 시작일 계산
let firstDayOfMonth = moment().startOf("month");
let currentMonday = firstDayOfMonth.clone().startOf("isoWeek");
if (currentMonday.month() !== firstDayOfMonth.month()) {
  currentMonday.add(7, "days");
}

const weeklyTitles = [];

while (currentMonday.month() === firstDayOfMonth.month() || currentMonday.clone().add(6, 'days').month() === firstDayOfMonth.month()) {
  const weeklyTitle = currentMonday.format("GGGG-[W]WW"); // ISO 주차 형식
  weeklyTitles.push(weeklyTitle);
  currentMonday.add(7, "days");
}

// 주차별 목표 동적으로 생성
weeklyTitles.forEach((weeklyTitle) => {
  output += `## [[${weeklyTitle}]] GOAL\n`;
  output += "- [*] \n\n";
});

output += "# SCHEDULES\n> [!info]- What the icon means\n> - [<] 일정\n> - [>] 미뤄진 일정\n> - [!] 중요한 일정\n> - [l] 오프라인 약속\n> - [w] 기념일\n";

// 월별 날짜 목록 생성
for (let day = 1; day <= daysInMonth; day++) {
  const date = moment().startOf("month").add(day - 1, 'days').format("YYYY-MM-DD");
  const dayName = moment(date).format("ddd");
  output += `- [<] (${dayName}) (@[[${date}]] 00:00PM) ⏳ ${date}\n`;
}

// 최종 출력
tR = output;

// 파일 이동
const destinationFolder = `LIFE/2025/MONTHLY NOTE`;
await tp.file.move(`${destinationFolder}/${title}`);
%>

# REVIEW
- [p] Good
- [b] Bad

# Etc.
> [!info]- 残る事  
> ![[투두리스트(백로그) + 기타#🍚 식사 목표 🍚]]


| Living | Family | Phone | Hair | Clothes | Etc. |
| ------ | ------ | ----- | ---- | ------- | ---- |
| 5      | 5      | 7     | 3    | 5       | 5    |

| House | Transportation |
| ----- | -------------- |
| 67    | 10             |
