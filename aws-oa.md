https://leetcode.com/discuss/interview-question/372434
```csharp
void Main()
{
//	int[] nums = new int[]{1,1,2,45,46,46};
		//int[] nums = new int[]{1,1};
			int[] nums = new int[]{1,5,1,5};
	int target = 6;
	
	Dictionary<int,int> dic = new Dictionary<int, int>();
	foreach(int num in nums)
	{
		if(dic.ContainsKey(num))
		{
			dic[num]++;
		}
		else
		{
			dic.Add(num,1);
		}
	}
	int count = 0;
	foreach(var kv in dic){
		if(kv.Key* 2 == target)
		{
			count += kv.Value- kv.Value %2;
			
		}
		else
		{
			if(dic.ContainsKey(target-kv.Key)){
				count = count + 1;
			}
		}
	}
	
	(count/2).Dump();
	
}

// Define other methods and classes here

```
