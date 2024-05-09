# Part 1

* A failure-inducing input
```
@Test
public void testReverseInPlace2() {
  int [] input1 = {1, 2, 3, 5, 6};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{6, 5, 3, 2, 1}, input1);
}
```
* An input that doesn't induce a failture
```
@Test 
public void testReverseInPlace() {
  int[] input1 = {1, 2, 3, 2, 1};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{1, 2, 3, 2, 1}, input1);
}
```
* The bug (before)
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```
* After
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```
* Explanation
The original buggy version fails to convert the second half of the values to the first half, because the first half already changed. This revision swaps both ends at the same time, and stops midpoint, so that no one would be missed out.

# Part 2

* `find` command
1. This finds files based on the dates that they are last modified. (in two cases, less than 1 day ago & more than 7 days ago, respectively)
```
froot@Lorins-Laptop technical % find . -name "*.txt" -mtime -1
    // nothing here
```
```
froot@Lorins-Laptop technical % find . -name "*.txt" -mtime +7
./plos/journal.pbio.0020046.txt
./plos/pmed.0020028.txt
./plos/journal.pbio.0020052.txt
./plos/pmed.0020148.txt
...    // too many to list them all
```
2. This finds files based on their sizes. (in two cases, bigger than 200 KB & smaller than 1 KB, respectively)
```
froot@Lorins-Laptop technical % find . -name "*.txt" -size +200k
./government/About_LSC/commission_report.txt
./government/Env_Prot_Agen/bill.txt
./government/Gen_Account_Office/GovernmentAuditingStandards_yb2002ed.txt
./government/Gen_Account_Office/Statements_Feb28-1997_volume.txt
./government/Gen_Account_Office/d01591sp.txt
./911report/chapter-13.4.txt
./911report/chapter-13.5.txt
./911report/chapter-3.txt
```
```
froot@Lorins-Laptop technical % find . -name "*.txt" -size -1k
./plos/pmed.0020191.txt
./plos/pmed.0020226.txt
```
3. This deletes files that meet the find requirements. (in two cases, files whose name contains "chapter" and "LegalServCorp" are deleted)
```
froot@Lorins-Laptop 911report % ls
chapter-1.txt           chapter-13.2.txt        chapter-3.txt           chapter-9.txt
chapter-10.txt          chapter-13.3.txt        chapter-5.txt           preface.txt
chapter-11.txt          chapter-13.4.txt        chapter-6.txt
chapter-12.txt          chapter-13.5.txt        chapter-7.txt
chapter-13.1.txt        chapter-2.txt           chapter-8.txt
froot@Lorins-Laptop 911report % find . -name "chapter*.txt" -delete
froot@Lorins-Laptop 911report % ls
preface.txt
```
```
froot@Lorins-Laptop About_LSC % ls                                         // list existing files for reference
CONFIG_STANDARDS.txt                    Special_report_to_congress.txt
Comments_on_semiannual.txt              State_Planning_Report.txt
LegalServCorp_v_VelazquezDissent.txt    State_Planning_Special_Report.txt
LegalServCorp_v_VelazquezOpinion.txt    Strategic_report.txt
LegalServCorp_v_VelazquezSyllabus.txt   commission_report.txt
ODonnell_et_al_v_LSCdecision.txt        conference_highlights.txt
ONTARIO_LEGAL_AID_SERIES.txt            diversity_priorities.txt
Progress_report.txt                     reporting_system.txt
Protocol_Regarding_Access.txt
froot@Lorins-Laptop About_LSC % find . -name "LegalServCorp*.txt" -delete  // delete
froot@Lorins-Laptop About_LSC % ls                                         // "LegalServCorp" files are gone
CONFIG_STANDARDS.txt                    State_Planning_Report.txt
Comments_on_semiannual.txt              State_Planning_Special_Report.txt
ODonnell_et_al_v_LSCdecision.txt        Strategic_report.txt
ONTARIO_LEGAL_AID_SERIES.txt            commission_report.txt
Progress_report.txt                     conference_highlights.txt
Protocol_Regarding_Access.txt           diversity_priorities.txt
Special_report_to_congress.txt          reporting_system.txt
```
4. This finds files up to a certain depth. (in two cases, depth 1 and 0 results in a list of folders within ./technical and nothing, respectively)
```
froot@Lorins-Laptop technical % find . -maxdepth 1        
.
./government
./.DS_Store
./plos
./biomed
./911report
```
```
froot@Lorins-Laptop technical % find . -maxdepth 0                                        
.
```

## Citation
The prompt I gave ChatGPT was: "Give me 16 interesting command-line potions or alternative ways to use the command `find`". And then I picked 4 out of them.
The original examples that I selected were the following:
* `find . -name "*.tmp" -delete`
* `find . -mtime +30`
* `find . -size +1M`
* `find . -type d -empty`
I incorporated the formatting, and changed all the commands into what fits the `./technical` directories and files.
