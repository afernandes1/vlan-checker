# vlan-checker
A python script to check if a vlan is configured in a specific equipment and interface. 


The script will open a xlsx file, containing a list of vlans to be checked against a specific equipment.

```python
dataframe = openpyxl.load_workbook("C:\\XXXXXX\\XXXXXX\\XXXXXX\\XXXXXX\\XXXXXX\\list_vlans.xlsx")
```

The command "show vlan id XXXX" where XXXX is the vlan id extracted from the xlsx file, can give us 3 different kinds of results.


Result 1 - Find the word "Po100" which is the interface we want to check:
If the result is != -1, it means the word "Po100" is present when we issue the command "show vlan id XXXX"

if output2.find("Po100") != -1:

Conclusion 1: vlan id XXXX in CORE and configured in the interface PO100


Result 2 - after issuing the command "show vlan id XXXX" we get "not found in current VLAN database":

elif output2.find("not found in current VLAN database") != -1:


Conclusion : It means the vlans XXXX is not present in this equipment


Result 3 - because we are using "If/Elif/Else" we know that if none of the 2 previous options are true, it means the vlan is present in the equipment but not configured in the Po100 interface.

Conclusion 3: vlan id XXXX configured in the equipment but not configured in interface Po100


The script will make this validation for all the vlans in the xlsx file.
For each vlans it checks, the script will write the results into a file called "Vlans_resultsFE.txt"
