# longest-common-subsequence-dp

def longest_common_subsequence(sequence1, sequence2):
    m = len(sequence1)
    n = len(sequence2)

    # Create DP table
    dp = [[0 for _ in range(n + 1)] for _ in range(m + 1)]

    # Fill DP table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if sequence1[i - 1] == sequence2[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

    # Reconstruct the LCS
    i, j = m, n
    lcs = []

    while i > 0 and j > 0:
        if sequence1[i - 1] == sequence2[j - 1]:
            lcs.append(sequence1[i - 1])
            i -= 1
            j -= 1
        elif dp[i - 1][j] > dp[i][j - 1]:
            i -= 1
        else:
            j -= 1

    lcs.reverse()

    return "".join(lcs)


# Take input from user
sequence1 = input("Enter the first sequence: ")
sequence2 = input("Enter the second sequence: ")

result = longest_common_subsequence(sequence1, sequence2)

print("\nLongest Common Subsequence:", result)
print("Length of LCS:", len(result))
