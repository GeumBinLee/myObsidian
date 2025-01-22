---
created: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
updated: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
tags:
  - weeklynote
---
<%*
const now = moment(); // 오늘 날짜 기준
const currentWeekMonday = now.clone().startOf('isoWeek'); // 이번 주 월요일 계산
const mon = currentWeekMonday.clone().add(0, 'days').format("YYYY-MM-DD");
const tue = currentWeekMonday.clone().add(1, 'days').format("YYYY-MM-DD");
const wed = currentWeekMonday.clone().add(2, 'days').format("YYYY-MM-DD");
const thu = currentWeekMonday.clone().add(3, 'days').format("YYYY-MM-DD");
const fri = currentWeekMonday.clone().add(4, 'days').format("YYYY-MM-DD");
const sat = currentWeekMonday.clone().add(5, 'days').format("YYYY-MM-DD");
const sun = currentWeekMonday.clone().add(6, 'days').format("YYYY-MM-DD");
const weekNumber = now.isoWeek(); // ISO 주차 계산
const weekYear = now.isoWeekYear(); // 해당 주차의 연도
const month = now.month() + 1;
const weeklyTitle = `${weekYear}년 ${month}월 ${weekNumber}주차`; // 위클리 제목 형식
const monthlyTitle = `${weekYear}-${String(month).padStart(2, "0")}`; // 월간 제목 형식
%>
# <% tp.file.title %>
## GOAL
- [*] 목표
```tasks
path includes LIFE/2025/MONTHLY NOTE/<% monthlyTitle %>
heading includes Week <% weekNumber %> GOAL
filter by function ["NON_TASK"].includes(task.status.type) && ["Star"].includes(task.status.name)
```

## 메모
- [n] 노트 테이킹
- [?] 질문
- [i] 정보성 메모
- [I] 아이디어
- [S] 재무 관련
- [b] 북마크
- ["] 인용

## UNFINISHED TASKS
```tasks
due on this week
filter by function ["TODO", "IN_PROGRESS"].includes(task.status.type) && !["Rescheduled", "Scheduled", "Location", "Cake", "Important"].includes(task.status.name)
```
```tasks
created on this week
(done after this week) OR (cancelled after this week)
filter by function ["DONE", "CANCELLED"].includes(task.status.type)
```

## REVIEW
- [p] Good
- [c] Bad

# TASKS BY DAYS OF THE WEEK
> [!Info] 위클리에서 데일리 업무를 추가할 경우, Tasks의 ➕와 📅 항목을 꼭 추가해야 함.
## [[<% mon %>]] (Mon)
### SCHEDULE for Mon
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
scheduled on <% mon %>
filter by function ['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
### TO DO LIST for Mon
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
due on <% mon %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% mon %>
heading includes "Today's tasks"
```
### MEMO for Mon
```tasks
path includes LIFE/2025/DAILY NOTE/<% mon %>
heading includes MEMO
```

## [[<% tue %>]] (Tue)
### SCHEDULE for Tue
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
scheduled on <% tue %>
filter by function ['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
### TO DO LIST for Tue
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
due on <% tue %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% tue %>
heading includes "Today's tasks"
```
### MEMO for Tue
```tasks
path includes LIFE/2025/DAILY NOTE/<% tue %>
heading includes MEMO
```

## [[<% wed %>]] (Wed)
### SCHEDULE for Wed
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
scheduled on <% wed %>
filter by function ['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
### TO DO LIST for Wed
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
due on <% wed %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% wed %>
heading includes "Today's tasks"
```
### MEMO for Wed
```tasks
path includes LIFE/2025/DAILY NOTE/<% wed %>
heading includes MEMO
```

## [[<% thu %>]] (Thu)
### SCHEDULE for Thu
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
scheduled on <% thu %>
filter by function ['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
### TO DO LIST for Thu
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
due on <% thu %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% thu %>
heading includes "Today's tasks"
```
### MEMO for Thu
```tasks
path includes LIFE/2025/DAILY NOTE/<% thu %>
heading includes MEMO
```

## [[<% fri %>]] (Fri)
### SCHEDULE for Fri
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
scheduled on <% fri %>
filter by function ['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
### TO DO LIST for Fri
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
due on <% fri %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% fri %>
heading includes "Today's tasks"
```
### MEMO for Fri
```tasks
path includes LIFE/2025/DAILY NOTE/<% fri %>
heading includes MEMO
```

## [[<% sat %>]] (Sat)
### SCHEDULE for Sat
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
scheduled on <% sat %>
filter by function ['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
### TO DO LIST for Sat
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
due on <% sat %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% sat %>
heading includes "Today's tasks"
```
### MEMO for Sat
```tasks
path includes LIFE/2025/DAILY NOTE/<% sat %>
heading includes MEMO
```

## [[<% sun %>]] (Sun)
### SCHEDULE for Sun
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
scheduled on <% sun %>
filter by function ['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
### TO DO LIST for Sun
```tasks
path does not include LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
due on <% sun %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% sun %>
heading includes "Today's tasks"
```
### MEMO for Sun
```tasks
path includes LIFE/2025/DAILY NOTE/<% sun %>
heading includes MEMO
```