### 微软笔试
1. https://leetcode.com/discuss/interview-question/365872/
```csharp

void Main()
{
//	int[] array = new int[]{42,33,60};
//	var array = new int[] { 51, 71, 17,42 };
	var array = new int[] { 51, 32,43 };
	this.maxSum(array).Dump();
}

class Pair
{
	public int? FirstNumber { get; set;}
	public int? SecondNumber {get;set;}
}

int maxSum(int[] array){

	if(array == null || array.Length <= 1 )
		return -1;
		
	Dictionary<int,Pair> dic = new Dictionary<int, Pair>();
	int res = int.MinValue;
	
	for(int i = 0;i<array.Length;i++){
	
		int sum = this.digit_sum(array[i]);
		
		if (!dic.ContainsKey(sum))
		{
			var pair = new Pair() { FirstNumber = array[i] };
			dic[sum] = pair;
			
		}
		else
		{
			var existing_pair = dic[sum];
			
			if(!existing_pair.SecondNumber.HasValue){
				
				existing_pair.SecondNumber = array[i];
				existing_pair.Dump();
				
			}
			else
			{
				var temp = Math.Max(existing_pair.FirstNumber.Value,existing_pair.SecondNumber.Value);
				existing_pair.SecondNumber = Math.Max(Math.Min(existing_pair.FirstNumber.Value,existing_pair.SecondNumber.Value), array[i]);
				existing_pair.FirstNumber = temp;
			}
			
			res = Math.Max(res,existing_pair.FirstNumber.Value+ existing_pair.SecondNumber.Value);
			
		}
	}
	
	return res == int.MinValue ? -1: res;
	
}

int digit_sum(int n)
{

	int sum = 0;
	while (n > 0)
	{
		sum += n % 10;
		n /= 10;
	}
	return sum;

}

```

2. https://leetcode.com/discuss/interview-question/398026/
```csharp
void Main()
{
	var s = "aab";
	int res = 0;
	int i = 0;
	while(i < s.Length)
	{
		int next = i + 1;
		while (next < s.Length && s[i] == s[next])
			next++;
		res += (next - i) / 3;
		
		i = next;
	}
	res.Dump();
}
```
3. [Max Network Rank](https://leetcode.com/discuss/interview-question/364760/) 
```csharp

void Main()
{
	int[] A = new int[]{1,2,3,3};
	int[] B = new int[]{2,3,1,4};
	int N = 4;
	this.maxNetworkRank(A,B,N).Dump();
}

int maxNetworkRank(int[] A, int[] B, int N)
{
	Dictionary<string,int> dic = new Dictionary<string,int>();
	Dictionary<string,int> dic2 = new Dictionary<string,int>();
	Dictionary<int,int> degree_dic = new Dictionary<int,int>();
	
	for (int i = 0; i < A.Length; i++)
	{
		string key = A[i] + ":" + B[i];
		dic[key] = 0;

		if (!degree_dic.ContainsKey(A[i])){
			degree_dic[A[i]] =1;
		}
		else
		{
			degree_dic[A[i]] +=1;
		}

		if (!degree_dic.ContainsKey(B[i]))
		{
			degree_dic[B[i]] = 1;
		}
		else
		{
			degree_dic[B[i]] += 1;
		}
	}

	foreach(var key in dic.Keys)
	{
		var index1 = Int32.Parse(key.Split(':')[0]);
		var index2 = Int32.Parse(key.Split(':')[1]);
		
		dic2[key] = degree_dic[index1] + degree_dic[index2];
	
		
	}
	
	return dic2.Values.Max()-1;
	}
```
3. Given a string S, find the largest alphabetic character, whose both uppercase and lowercase appear in S. The uppercase character should be returned. For example, for S = "admeDCAB", return "D". If there is no such character, return "NO".

```csharp
string test = "abcFdCfABC";
 	 //两次循环,能不能改一次循环呢? 
	Dictionary<int,bool> map = new Dictionary<int,bool>();
	int result = -1;  
	foreach (var c in test)
	{
		int key = c - 0; 

		if (!map.ContainsKey(key))
			map[key] = true;
	}
	
	foreach (var c in test)
	{
		int key = c - 0;

		if (Char.IsLower(c) && map.ContainsKey(key - 32))
		{
			result = Math.Max(result, key - 32);
		}
		else if (!Char.IsLower(c) && map.ContainsKey(key + 32))
		{
			result = Math.Max(result, key);
		}
	}
	
	var ret = result == -1? "NO": ((char)result).ToString();
	ret.Dump();
```
