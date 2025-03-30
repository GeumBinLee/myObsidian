---
created: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
updated: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
tags:
  - weeklynote
---
<%*
const now = moment(); // 오늘 날짜 기준
const currentWeekMonday = now.clone().startOf('isoWeek'); // 이번 주 월요일 계산
const nextWeekMonday = currentWeekMonday.clone().add(7, 'days'); // 다음 주 월요일
const previousWeekMonday = currentWeekMonday.clone().subtract(7, 'days'); // 이전 주 월요일

// 현재 주의 모든 요일 가져오기
const weekDays = Array.from({ length: 7 }, (_, i) => currentWeekMonday.clone().add(i, 'days'));
const monthCounts = {};
weekDays.forEach(day => {
    const monthKey = `${day.year()}-${String(day.month() + 1).padStart(2, "0")}`;
    monthCounts[monthKey] = (monthCounts[monthKey] || 0) + 1;
});

// 가장 많은 일수를 포함하는 달 찾기
let assignedMonth = Object.entries(monthCounts).reduce((a, b) => (b[1] > a[1] ? b : a))[0];
const [assignedYear, assignedMonthNum] = assignedMonth.split('-').map(Number);

// 해당 월의 첫 번째 월요일 찾기
const monthStart = moment(`${assignedYear}-${String(assignedMonthNum).padStart(2, "0")}-01`).startOf('month');
let firstMonday = monthStart.clone().startOf('isoWeek');
if (firstMonday.month() + 1 !== assignedMonthNum) {
    firstMonday.add(7, 'days');
}

// 해당 월의 몇 번째 주인지 계산
const weekIndexInMonth = currentWeekMonday.diff(firstMonday, 'weeks') + 1;

// 주차 제목 설정 (월 기준 주차 적용)
const weeklyTitle = `${assignedYear}-${String(assignedMonthNum).padStart(2, "0")}-W${String(weekIndexInMonth).padStart(2, "0")}`;
const header = `${assignedYear}년 ${assignedMonthNum}월 ${weekIndexInMonth}주차`;
const monthlyTitle = `${assignedYear}-${String(assignedMonthNum).padStart(2, "0")}`;

// 전주 및 다음 주 계산
const previousWeekTitle = previousWeekMonday.clone().year() + '-' + String(previousWeekMonday.clone().month() + 1).padStart(2, "0") + '-W' + String(previousWeekMonday.clone().diff(firstMonday, 'weeks') + 1).padStart(2, "0");
const nextWeekTitle = nextWeekMonday.clone().year() + '-' + String(nextWeekMonday.clone().month() + 1).padStart(2, "0") + '-W' + String(nextWeekMonday.clone().diff(firstMonday, 'weeks') + 1).padStart(2, "0");

// 기존 주차 파일이 있으면 덮어쓰지 않도록 설정
const destinationFolder = `LIFE/${assignedYear}/WEEKLY NOTE`;
const filePath = `${destinationFolder}/${weeklyTitle}`;
if (!(await app.vault.adapter.exists(filePath))) {
    await tp.file.move(filePath);
}
%>
> [!Note] 🏃🏻‍♀️Go to page🏃🏻‍♀️
> LAST WEEK ➡️ [[<% previousWeekTitle %>]]
> NEXT WEEK ➡️ [[<% nextWeekTitle %>]]
> MONTHLY NOTE ➡️ [[<% assignedYear %>-<% String(assignedMonthNum).padStart(2, "0") %>]]

# <% header %>
## GOAL
> [!NOTE] 주간 목표 in 월간 다이어리
> ```tasks
> path includes LIFE/2025/MONTHLY NOTE/<% monthlyTitle %>
> heading includes <% weeklyTitle %>
> filter by function (['NON_TASK'].includes(task.status.type) && ['Star'].includes(task.status.name)) || (['DONE', 'CANCELLED'].includes(task.status.type)) || (['Rescheduled']).includes(task.status.name)
> ```
- [*] 완수함
- [>] 어느 정도 하긴 했지만 100% 달성하진 못함 (다음 주에 이어서 처리해야 함)
- [-] 아예 달성하지 못함

## REVIEW
- [p] Good
- [c] Bad

## UNFINISHED TASKS
```tasks
due on or after <% currentWeekMonday.format("YYYY-MM-DD") %>
due on or before <% currentWeekMonday.clone().add(6, 'days').format("YYYY-MM-DD") %>
due on or before today
filter by function ['TODO', 'IN_PROGRESS'].includes(task.status.type) && !['Rescheduled', 'Scheduled', 'Location', 'Cake', 'Important'].includes(task.status.name)
```
```tasks
created after <% currentWeekMonday.clone().subtract(1, 'days').format("YYYY-MM-DD") %>
created before <% currentWeekMonday.clone().add(7, 'days').format("YYYY-MM-DD") %>
(done after <% currentWeekMonday.clone().add(6, 'days').format("YYYY-MM-DD") %>) OR (cancelled after <% currentWeekMonday.clone().add(6, 'days').format("YYYY-MM-DD") %>)
filter by function ['DONE', 'CANCELLED'].includes(task.status.type)
```

# SCHEDULE by days of the week
```tasks
filter by function task.scheduled !== null && task.scheduled.format('YYYY-MM-DD') >= '<% currentWeekMonday.format("YYYY-MM-DD") %>' && task.scheduled.format('YYYY-MM-DD') <= '<% currentWeekMonday.clone().add(6, 'days').format("YYYY-MM-DD") %>' && task.originalMarkdown.includes('⏳')
group by scheduled
```

# TASKS AND MEMO by days of the week
> [!Info] 위클리에서 데일리 업무를 추가할 경우, Tasks의 ➕와 📅 항목을 꼭 추가해야 함.
<%* for (let i = 0; i < 7; i++) { let day = currentWeekMonday.clone().add(i, 'days').format("YYYY-MM-DD"); let dayName = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"][i]; %>
## 🗂️ [[<% day %>]] (<% dayName %>)
> [!example] TO DO LIST for <% dayName %>
> ```tasks
> path does not include "LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>"
> due on <% day %>
> filter by function !(task.file.path.includes("LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>") && task.heading?.includes("<% dayName %>"))
> filter by function ['TODO', 'IN_PROGRESS', 'DONE', 'CANCELLED'].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
> ```

> [!example] MEMO for <% dayName %>
> ```tasks
> path includes LIFE/2025/DAILY NOTE/<% String(assignedMonthNum).padStart(2, "0") %>/<% day %>
> heading includes MEMO
> ```
<%* } %>