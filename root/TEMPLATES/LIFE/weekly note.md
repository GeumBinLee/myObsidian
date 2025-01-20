<%*
const now = moment(); // 오늘 날짜 기준
const currentWeekMonday = now.clone().startOf('isoWeek'); // 이번 주 월요일 계산
%>

# <% tp.file.title %> 

## TO DO LIST
```tasks
not done
path includes <% tp.file.folder(true) %>/<% tp.file.title %>
```

## MEMO
- 

## 일간 노트
- [[<% currentWeekMonday.clone().add(0, 'days').format("YYYY-MM-DD (ddd)") %>]] (월요일)
- [[<% currentWeekMonday.clone().add(1, 'days').format("YYYY-MM-DD (ddd)") %>]] (화요일)
- [[<% currentWeekMonday.clone().add(2, 'days').format("YYYY-MM-DD (ddd)") %>]] (수요일)
- [[<% currentWeekMonday.clone().add(3, 'days').format("YYYY-MM-DD (ddd)") %>]] (목요일)
- [[<% currentWeekMonday.clone().add(4, 'days').format("YYYY-MM-DD (ddd)") %>]] (금요일)
- [[<% currentWeekMonday.clone().add(5, 'days').format("YYYY-MM-DD (ddd)") %>]] (토요일)
- [[<% currentWeekMonday.clone().add(6, 'days').format("YYYY-MM-DD (ddd)") %>]] (일요일)
