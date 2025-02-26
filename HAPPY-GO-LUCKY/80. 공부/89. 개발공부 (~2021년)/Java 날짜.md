---
Created: Invalid date
Updated: Invalid date
---
- 지금 날짜랑 시간

new SimpleDateFormat("yyyy-MM-dd hh:mm:ss").format(new Date(System.currentTimeMillis()));

- 전 년월

// 전년월 구하기  
SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM");  
Calendar cal = Calendar.getInstance();  
cal.add(Calendar.MONTH, -1);  
String month = dateFormat.format(cal.getTime());  

- 오늘부터

//String checked = "WEEK";  
String checked = "MONTH";  
List<String> dateList = new ArrayList<>();  
String fromDateStr = "2014-06-13";  
String[] dateArr = fromDateStr.split("-");int year = Integer.parseInt(dateArr[0]);int month = Integer.parseInt(dateArr[1]) - 1;int date = Integer.parseInt(dateArr[2]);  
Calendar cal = Calendar.getInstance();  
cal.set(year, month, date);int y = cal.get(Calendar.YEAR);int w = cal.get(Calendar.WEEK_OF_MONTH);int m = cal.get(Calendar.MONTH);if(checked.equals("WEEK")){  
String label;  
label = (m+1) + "월" + w + "주";//if(w == 1)label = (m+1) + "월" + w + "주";//else label = w + "주";  
dateList.add(label);  
} else if(checked.equals("MONTH")) {  
String label;  
label = String.valueOf(y).substring(2,4) + "년" + (m+1) + "월";//if(m == 0)label = String.valueOf(y).substring(2,4) + "년" + (m+1) + "월";//else label = (m+1) + "월";  
dateList.add(label);  
}for(String str : dateList) {  
System.out.println("str : " + str);  
}  

/** 하루전 날짜 가져오기

* @return 하루전 날짜

*/

public static String getYesterday(){

Calendar calendar = new GregorianCalendar(Locale.KOREA);

java.util.Date trialTime = new java.util.Date();

calendar.setTime(trialTime);

// 하루 전 날짜로 계산 하기 위한 메소드

calendar.add(Calendar.DATE, -1);

String year = String.valueOf(calendar.get(Calendar.YEAR));

String month = String.valueOf(calendar.get(Calendar.MONTH) + 1);

String date = String.valueOf(calendar.get(Calendar.DATE));

if(month.length() < 2) month = "0" + month;

if(date.length() < 2) date = "0" + date;

return year + month + date;

}

이 해당 메소드의 빨간색 부분을 아래 내용으로 수정해 보시라...

calendar.add(Calendar.DATE, 2); // 이틀후

calendar.add(Calendar.YEAR, 2); // 2년 후

calendar.add( Calendar.MONTH, 2); // 2달 후