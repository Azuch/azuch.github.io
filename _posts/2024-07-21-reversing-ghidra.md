ok, today i gonna re the wannacry;
first load it in ghidra with the following setting:
	1. Decompiler Parameter ID. Why? According to the internet (i believe in you, pal): https://reverseengineering.stackexchange.com/questions/24633/function-prototypes-given-by-ghidra-is-not-consistent
		"So, I found out the reason. By default when the ghidra asks for options when we load the binary, Decompiler Parameter ID option is disabled. Once you enable it, you will have the function parameters correctly. It will take longer time to make the analysis once this option is enabled." 
	2. WindowsPE x86 Propagate External Parameters. Why? According to the internet (again): 
 		"On first glance, one feature I missed from IDA was the comments where IDA gave me the names of parameters for Windows API calls (e.g., the first parameter to RegOpenKeyExA in MSDN is listed as hKey with a type HKEY). It turns out Ghidra can do this to. It requires changing one of the defaults in the AutoAnalysis settings (you see this when you first open a file for analysis or when you choose AutoAnalysis from the Analysis menu). The option WindowsPE x86 Propagate External Parameters is disabled by default, if you enable this option then you get the comments you expect."
   	![image](https://github.com/user-attachments/assets/a1c2e49e-3afe-4a12-9a1e-b36d66fd0d04)
	//As a resource, you can read it from here: https://isc.sans.edu/diary/A+few+Ghidra+tips+for+IDA+users+part+0+automatic+comments+for+API+call+parameters/24806
 The, after loading it, let find the entry point. Why not main or winMain you may ask? Because i find it more consitence

 the datatype for change winmain:
 	“Data Type Manager” allows you to see all specific types, including built-in ones, specific for the binary file and other types included Ghidra (for example, those we see in Windows called “windows_vs12_32”). Try unpacking the book icons and right-clicking on Data Type. Then click “Find Uses of” to see where this data type is used in the binary file. 
  	More sources: https://www.shogunlab.com/blog/2019/04/12/here-be-dragons-ghidra-0.html
   
