~~~java
import java.util.ArrayList;
import java.util.Calendar;
import java.util.List;

public class DayOfWeek {
    public static void main(String[] args) {
        Calendar today = Calendar.getInstance();

        int year = 2020;
        int month = 5;
        int day = 1;

        List<Integer> dayOfList = new ArrayList<Integer>();

        //날짜 셋팅
        today.set(year, month -1, day);
        
        //해당 월의 마지막 일
        int maximum = today.getActualMaximum(Calendar.DAY_OF_MONTH);
        
        //주말
        for(int minimum = 1 ; minimum <= maximum ; minimum++) {
            today.set(Calendar.DATE, minimum);
            
            int dayOfWeek = today.get(Calendar.DAY_OF_WEEK);

            if(dayOfWeek == 1 || dayOfWeek == 7) {
                dayOfList.add(minimum);
            }
        }

        System.out.println(dayOfList.toString());
    }
}
~~~