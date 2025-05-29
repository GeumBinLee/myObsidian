---
created: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
updated: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
tags:
  - monthlynote
score:
---
<%*
const fileTitle = tp.file.title; // 예: '2025-06'
const current = moment(fileTitle, "YYYY-MM");
const title = current.format("YYYY-MM");
const year = current.format("YYYY");
const daysInMonth = current.daysInMonth();
const prevMonth = current.clone().subtract(1, "month").format("YYYY-MM");
const nextMonth = current.clone().add(1, "month").format("YYYY-MM");

let output = `> [!note] Go to Page\n> LAST MONTH ⭢ [[${prevMonth}]]\n> NEXT MONTH ⭢ [[${nextMonth}]]\n\n`;

output += `# GOALS\n`;
output += "> [!note] 이번 달 목표\n> - [*] \n> - [*] \n> - [*] \n\n";

// ISO 기준 주차 계산
let firstDayOfMonth = current.clone().startOf("month");
let currentMonday = firstDayOfMonth.clone().startOf("isoWeek");
if (currentMonday.month() !== firstDayOfMonth.month()) {
  currentMonday.add(7, "days");
}

const weeklyTitles = [];
while (
  currentMonday.month() === firstDayOfMonth.month() ||
  currentMonday.clone().add(6, "days").month() === firstDayOfMonth.month()
) {
  const weeklyTitle = currentMonday.format("GGGG-[W]WW");
  weeklyTitles.push(weeklyTitle);
  currentMonday.add(7, "days");
}

weeklyTitles.forEach((weeklyTitle) => {
  output += `## [[${weeklyTitle}]] GOAL\n`;
  output += "- [*] \n\n";
});

output += `# SCHEDULES\n> [!info]- What the icon means\n> - [<] 일정\n> - [>] 미루어진 일정\n> - [!] 중요한 일정\n> - [l] 오프라인 약속\n> - [w] 기념일\n`;

for (let day = 1; day <= daysInMonth; day++) {
  const date = current.clone().startOf("month").add(day - 1, "days").format("YYYY-MM-DD");
  const dayName = moment(date).format("ddd");
  output += `- [<] (${dayName}) (@[[${date}]] 00:00PM) ⏳ ${date}\n`;
}

output += `\n# REVIEW\n- [p] Good\n- [b] Bad\n\n`;

output += `# Etc.\n`;
output += `> [!info]- 残る事\n`;
output += `> ![[투두리스트(백로그) + 기타#🍚 식사 목표 🍚]]\n\n`;

output += `| Living | Family | Phone | Hair | Clothes | Etc. |\n`;
output += `| ------ | ------ | ----- | ---- | ------- | ---- |\n`;
output += `| 5      | 5      | 7     | 3    | 5       | 5    |\n\n`;

output += `| House | Transportation |\n`;
output += `| ----- | -------------- |\n`;
output += `| 67    | 10             |\n`;

tR = output;

// 파일 이동
const destinationFolder = `LIFE/${year}/MONTHLY NOTE`;
const fullPath = `${destinationFolder}/${title}.md`;

if (!(await app.vault.adapter.exists(fullPath))) {
  await tp.file.move(fullPath);
} else {
  new Notice(`📄 이미 존재하는 월간 노트: ${title}`);
}
%>
