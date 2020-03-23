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
