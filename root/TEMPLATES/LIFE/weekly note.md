<%*
const now = moment(); // 오늘 날짜 기준
const currentWeekMonday = now.clone().startOf('isoWeek'); // 이번 주 월요일 계산
const mon = currentWeekMonday.clone().add(0, 'days').format("YYYY-MM-DD (ddd)");
const tue = currentWeekMonday.clone().add(1, 'days').format("YYYY-MM-DD (ddd)");
const wed = currentWeekMonday.clone().add(2, 'days').format("YYYY-MM-DD (ddd)");
const thu = currentWeekMonday.clone().add(3, 'days').format("YYYY-MM-DD (ddd)");
const fri = currentWeekMonday.clone().add(4, 'days').format("YYYY-MM-DD (ddd)");
const sat = currentWeekMonday.clone().add(5, 'days').format("YYYY-MM-DD (ddd)");
const sun = currentWeekMonday.clone().add(6, 'days').format("YYYY-MM-DD (ddd)");
%>
# <% tp.file.title %>
## MEMO
- [n] 노트 테이킹
- [*] 중요 메모
- [?] 질문
- [i] 정보성 메모
- [I] 아이디어
- [S] 재무 관련
- [b] 북마크
- ["] 인용

## PRIORITY
- 

## POSTPONED TASKS for this week
```tasks
due on this week
created before this week
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```

## UNFINISHED TASKS
```tasks
path includes LIFE/2025/DAILY NOTE
due on this week
filter by function ["TODO", "IN_PROGRESS"].includes(task.status.type) && !["Rescheduled", "Scheduled", "Location", "Cake", "Important"].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE
created on this week
(done after this week) OR (cancelled after this week)
filter by function ["DONE", "CANCELLED"].includes(task.status.type)
```

## REVIEW
- [p] Good
- [c] Bad

# TASKS BY DAYS OF THE WEEK
> [!Info] 위클리에서 데일리 업무를 추가할 경우, Tasks의 ➕와 📅 항목을 꼭 추가해야 함.
## [[<% mon %>]]
```tasks
path includes LIFE/2025/DAILY NOTE/<% mon %>
heading includes SCHEDULE
```
```tasks
due on <% mon %>
created before <% mon %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% mon %>
heading includes TO DO LIST
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% mon %>
heading includes MEMO
```

## [[<% tue %>]]
```tasks
path includes LIFE/2025/DAILY NOTE/<% tue %>
heading includes SCHEDULE
```
```tasks
due on <% tue %>
created before <% tue %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% tue %>
heading includes TO DO LIST
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% tue %>
heading includes MEMO
```

## [[<% wed %>]]
```tasks
path includes LIFE/2025/DAILY NOTE/<% wed %>
heading includes SCHEDULE
```
```tasks
due on <% wed %>
created before <% wed %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% wed %>
heading includes TO DO LIST
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% wed %>
heading includes MEMO
```

## [[<% thu %>]]
```tasks
path includes LIFE/2025/DAILY NOTE/<% thu %>
heading includes SCHEDULE
```
```tasks
due on <% thu %>
created before <% thu %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% thu %>
heading includes TO DO LIST
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% thu %>
heading includes MEMO
```

## [[<% fri %>]]
```tasks
path includes LIFE/2025/DAILY NOTE/<% fri %>
heading includes SCHEDULE
```
```tasks
due on <% fri %>
created before <% fri %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% fri %>
heading includes TO DO LIST
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% fri %>
heading includes MEMO
```

## [[<% sat %>]]
```tasks
path includes LIFE/2025/DAILY NOTE/<% sat %>
heading includes SCHEDULE
```
```tasks
due on <% sat %>
created before <% sat %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% sat %>
heading includes TO DO LIST
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% sat %>
heading includes MEMO
```

## [[<% sun %>]]
```tasks
path includes LIFE/2025/DAILY NOTE/<% sun %>
heading includes SCHEDULE
```
```tasks
due on <% sun %>
created before <% sun %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% sun %>
heading includes TO DO LIST
```
```tasks
path includes LIFE/2025/DAILY NOTE/<% sun %>
heading includes MEMO
```
