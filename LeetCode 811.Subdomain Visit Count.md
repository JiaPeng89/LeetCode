## LeetCode 811.Subdomain Visit Count

### Problem :

A website domain like "discuss.leetcode.com" consists of various subdomains. At the top level, we have "com", at the next level, we have "leetcode.com", and at the lowest level, "discuss.leetcode.com". When we visit a domain like "discuss.leetcode.com", we will also visit the parent domains "leetcode.com" and "com" implicitly.

Now, call a "count-paired domain" to be a count (representing the number of visits this domain received), followed by a space, followed by the address. An example of a count-paired domain might be "9001 discuss.leetcode.com".

We are given a list **`cpdomains`** of count-paired domains. We would like a list of count-paired domains, (in the same format as the input, and in any order), that explicitly counts the number of visits to each subdomain.

```python
Example 1:
Input: 
["9001 discuss.leetcode.com"]
Output: 
["9001 discuss.leetcode.com", "9001 leetcode.com", "9001 com"]
Explanation: 
We only have one website domain: "discuss.leetcode.com". As discussed above, the subdomain "leetcode.com" and "com" will also be visited. So they will all be visited 9001 times.
```

```python
Example 2:
Input: 
["900 google.mail.com", "50 yahoo.com", "1 intel.mail.com", "5 wiki.org"]
Output: 
["901 mail.com","50 yahoo.com","900 google.mail.com","5 wiki.org","5 org","1 intel.mail.com","951 com"]
Explanation: 
We will visit "google.mail.com" 900 times, "yahoo.com" 50 times, "intel.mail.com" once and "wiki.org" 5 times. For the subdomains, we will visit "mail.com" 900 + 1 = 901 times, "com" 900 + 50 + 1 = 951 times, and "org" 5 times.
```

**Notes:**

- The length of **`cpdomains` **will not exceed **`100`**. 
- The length of each domain name will not exceed **`100`**.
- Each address will have either 1 or 2 "." characters.
- The input count in any count-paired domain will not exceed **`10000`**.
- The answer output can be returned in any order.

### Solution :

my first submission code is:

```python
class Solution:
    def subdomainVisits(self, cpdomains):
        """
        :type cpdomains: List[str]
        :rtype: List[str]
        """
        dict={}
        for i,element in enumerate(cpdomains):
            count,domain = element.split(" ",2)
            subindex1 = domain.rfind(".")
            sub1 = domain[subindex1+1:]
            subindex2 = domain.find(".")
            sub2 = domain[subindex2+1:]
            if(domain in dict):
                dict[domain] += int(count)
            else:
                dict[domain] = int(count)

            if(sub1 in dict):
                dict[sub1] += int(count)
            else:
                dict[sub1] = int(count)

            if sub1 != sub2:
                if(sub2 in dict):
                    dict[sub2] += int(count)
                else:
                    dict[sub2] = int(count)     

        list = []
        for i in range(len(dict)):
            pop_obj = dict.popitem()
            pairs = str(pop_obj[1]) + " " + pop_obj[0]
            list.append(pairs)
            
        return list
```

after checking other people's python code , for simplicity, I have refined it to :

```python
class Solution:
    def subdomainVisits(self, cpdomains):
        """
        :type cpdomains: List[str]
        :rtype: List[str]
        """
        dict={}
        for i in cpdomains:
            snum, address = i.split(' ')
            num = int(snum)
            addr = address.split('.')
            n = len(addr)
            for j in range(n):
                domain = '.'.join(addr[j:])
                if(domain in dict):
                    dict[domain] += num
                else:
                    dict[domain] = num
       
        list = []
        for key in dict:
            list.append(str(dict[key]) + ' ' + key)
            
        return list
```

explatory-free code.