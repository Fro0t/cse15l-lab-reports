## Student Screenshots
![image](https://github.com/Fro0t/cse15l-lab-reports/assets/165719298/fbf407a7-83b3-46f3-909f-ef364de54cbe)

`Code.java` has following contents:
```
import java.io.File;

public class Code {
   public static void main(String[] args) {
       File file = new File(args[0]);
       if (file.exists()) {
           System.out.println("File exists, yay!");
       }
       else {
           System.out.println("The file does not exist :(");
       }
   }
}
```

Symptoms after trying to run `Code.java`

![image](https://github.com/Fro0t/cse15l-lab-reports/assets/165719298/ef1e803f-c277-41ba-9e58-3de01e703bde)
