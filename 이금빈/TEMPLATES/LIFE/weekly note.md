---
created: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
updated: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
tags:
  - weeklynote
---


<%*
let title = tp.file.title;
const isoWeekTitle = moment().format("GGGG-[W]WW");

if (!/^(\d{4})-W(\d{2})$/.test(title)) {
  await tp.file.rename(isoWeekTitle);
  title = isoWeekTitle;
}

const currentWeekMonday = moment(title, "GGGG-[W]WW").startOf("isoWeek");
const weekStart = currentWeekMonday.format("YYYY-MM-DD");
const weekEnd = currentWeekMonday.clone().add(6, "days").format("YYYY-MM-DD");
const prevWeek = currentWeekMonday.clone().subtract(1, "week");
const nextWeek = currentWeekMonday.clone().add(1, "week");
const monthNote = currentWeekMonday.clone().startOf("month");

const prevTitle = prevWeek.format("GGGG-[W]WW");
const nextTitle = nextWeek.format("GGGG-[W]WW");
const monthlyTitle = monthNote.format("YYYY-MM");

let result = `# ✈️ Go to page\n
> [!Note] 🏃🏻‍♀️Go to another page🏃🏻‍♀️  
> LAST WEEK ➡️ [[${prevTitle}]]  
> NEXT WEEK ➡️ [[${nextTitle}]]  
> MONTHLY NOTE ➡️ [[${monthlyTitle}]]\n
`;

const dayNames = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

// 요일 빠른 이동 링크 생성
result += `> [!note] 📅 Jump to Day 📅\n> `;
for (let i = 0; i < 7; i++) {
  const currentDay = currentWeekMonday.clone().add(i, 'days');
  const day = currentDay.format("YYYY-MM-DD");
  const dayName = dayNames[i];
  result += `[[# 🗂️ ${day} (${dayName})|${dayName}]]`;
  if (i < 6) result += ' • ';
}
result += `\n\n`;

result += `# 🏁 GOAL
> [!note] Weekly Goal in Monthly Note
> \`\`\`tasks
> path includes LIFE/${currentWeekMonday.format("YYYY")}/MONTHLY NOTE/${monthlyTitle}
> heading includes ${title}
> filter by function (['NON_TASK'].includes(task.status.type) && ['Star'].includes(task.status.name)) || (['DONE', 'CANCELLED'].includes(task.status.type)) || (['Rescheduled']).includes(task.status.name)
> \`\`\`
- [*] 완수함
- [>] 어느 정도 하긴 했지만 100% 달성하진 못함 (다음 주에 이어서 처리해야 함)
- [-] 아예 달성하지 못함
`;

for (let i = 0; i < 7; i++) {
  const currentDay = currentWeekMonday.clone().add(i, 'days');
  const day = currentDay.format("YYYY-MM-DD");
  const dayName = dayNames[i];

  result += `
# 🗂️ ${day} (${dayName})
> [!info] [[#✈️ Go to page|페이지 or 요일 이동 버튼]]

> [!note] MEAL
> - ⛅️ 아침 ⛅️: 
> - ☀️ 점심 ☀️: 
> - 🌕 저녁 🌕: 

> [!note] SCHEDULE
> \`\`\`tasks
> scheduled on ${day}
> filter by function !["Pro", "Con"].includes(task.status.name)
> \`\`\`

> [!note] Postponed tasks for ${day}
> \`\`\`tasks
> due on ${day}
> created before ${day}
> filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !["Scheduled", "Rescheduled", "Important", "Location", "Cake"].includes(task.status.name)
> \`\`\`

> [!note] Tasks created on ${day}
> \`\`\`tasks
> path does not include LIFE/${currentDay.format("YYYY")}/WEEKLY NOTE/${title}
> # due on ${day} # 원래 쿼리
> happens on ${day}
> created on or after ${day}
> filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !["Scheduled", "Rescheduled", "Important", "Location", "Cake"].includes(task.status.name)
> \`\`\`
> - [ ] 운동 - ➕ ${day} 📅 ${day}
> - [ ] 스트레칭 - ➕ ${day} 📅 ${day}
> - [ ] #일본어 (Anki) 日本語 勉強 ➕ ${day} 📅 ${day}
> - [ ] #영어 (Anki) Studying English ➕ ${day} 📅 ${day}
> - [ ] 독서 - 「책 제목」 ➕ ${day} 📅 ${day}

> [!info] 세부사항 작성을 원할 경우 파일 생성 (메모, 감사 노트, 일기, 리뷰)
> [[LIFE/${currentDay.format("YYYY")}/DAILY NOTE/${currentDay.format("MM")}/${day}.md]]
`;
}

result += `
# 📚 UNFINISHED TASKS
> [!note] UNFINISHED TASKS
> \`\`\`tasks
> due on or after ${weekStart}
> due on or before ${weekEnd}
> due on or before today
> filter by function ['TODO', 'IN_PROGRESS'].includes(task.status.type) && !['Rescheduled', 'Scheduled', 'Location', 'Cake', 'Important'].includes(task.status.name)
> \`\`\`
> 
> \`\`\`tasks
> created on or after ${weekStart}
> created on or before ${weekEnd}
> (done after ${weekEnd}) OR (cancelled after ${weekEnd})
> filter by function ['DONE', 'CANCELLED'].includes(task.status.type)
> \`\`\`
`;
tR += result;
%>
