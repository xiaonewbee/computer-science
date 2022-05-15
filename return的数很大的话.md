```
long ret = 0;
long M = 1e9+7;

for (int i = 0; i<n; i++)
{
	ret = (ret + (long)freq[i] * (long)nums[i]) % M;
}
```

1589 leetcode;

