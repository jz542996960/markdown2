```
#!/bin/bash
#

file=E:\\11.txt

awk -F ',' '{	
		if($53 == "giftStatus=1"){
			print $53 " " $77
		}
	}' $file
```

awk中条件选择

