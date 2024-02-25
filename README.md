# String-Value-Minimization
Given a string 's' composed of lowercase letters and an integer 'k', the task is to compute the minimum value of the string following the removal of 'k' characters. The value of the string is defined as the sum of the squared counts of each distinct character in the string.

import heapq
from collections import Counter

def min_string_value(s, k):
    counts = Counter(s)

    max_heap = [-count for count in counts.values()]
    heapq.heapify(max_heap)

    while k > 0:
        max_count = -heapq.heappop(max_heap)
        
        k -= 1

        updated_count = max(0, max_count - 1)

        if updated_count > 0:
            heapq.heappush(max_heap, -updated_count)

    result = sum(count ** 2 for count in max_heap)
    return result

s = input().strip()
k = int(input().strip())
output = min_string_value(s, k)
print(output)
