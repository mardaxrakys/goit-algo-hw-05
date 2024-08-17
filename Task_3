import timeit
#-------------------------------------------------------
def bad_char_heuristic(pattern):
    bad_char = {}
    for i, char in enumerate(pattern):
        bad_char[char] = i
    return bad_char

def boyer_moore_search(text, pattern):
    bad_char = bad_char_heuristic(pattern)
    m = len(pattern)
    n = len(text)
    s = 0
    while s <= n - m:
        j = m - 1
        while j >= 0 and pattern[j] == text[s + j]:
            j -= 1
        if j < 0:
            return s
        s += max(1, j - bad_char.get(text[s + j], -1))
    return -1
#---------------------------------------------------------
def compute_lps(pattern):
    lps = [0] * len(pattern)
    length = 0
    i = 1
    while i < len(pattern):
        if pattern[i] == pattern[length]:
            length += 1
            lps[i] = length
            i += 1
        else:
            if length != 0:
                length = lps[length - 1]
            else:
                lps[i] = 0
                i += 1
    return lps

def kmp_search(text, pattern):
    lps = compute_lps(pattern)
    i = 0
    j = 0
    while i < len(text):
        if pattern[j] == text[i]:
            i += 1
            j += 1
        if j == len(pattern):
            return i - j
        elif i < len(text) and pattern[j] != text[i]:
            if j != 0:
                j = lps[j - 1]
            else:
                i += 1
    return -1
#-------------------------------------------------------------
def rabin_karp_search(text, pattern, d=256, q=101):
    M = len(pattern)
    N = len(text)
    i = 0
    j = 0
    p = 0
    t = 0
    h = 1
    for i in range(M - 1):
        h = (h * d) % q
    for i in range(M):
        p = (d * p + ord(pattern[i])) % q
        t = (d * t + ord(text[i])) % q
    for i in range(N - M + 1):
        if p == t:
            if text[i:i + M] == pattern:
                return i
        if i < N - M:
            t = (d * (t - ord(text[i]) * h) + ord(text[i + M])) % q
            if t < 0:
                t += q
    return -1
#-----------------------------------------------------------------

# Функції для тестування
def time_search_algorithm(algorithm, text, pattern):
    start_time = timeit.default_timer()
    result = algorithm(text, pattern)
    end_time = timeit.default_timer()
    return end_time - start_time, result

# Встановіть текст і патерни
text1 = open("article1.txt").read()
text2 = open("article2.txt").read()
pattern_existing = "алгоритм"  # Приклад підрядка, який існує в текстах
pattern_non_existing = "неіснуючий"  # Приклад підрядка, який не існує

# Вимірювання часу
algorithms = {
    "Boyer-Moore": boyer_moore_search,
    "KMP": kmp_search,
    "Rabin-Karp": rabin_karp_search
}

results = {}

for name, algo in algorithms.items():
    for text_name, text in [("Article 1", text1), ("Article 2", text2)]:
        for pattern in [pattern_existing, pattern_non_existing]:
            time_taken, _ = time_search_algorithm(algo, text, pattern)
            results[f"{name} - {text_name} - {'Existing' if pattern == pattern_existing else 'Non-existing'}"] = time_taken

# Вивід результатів
for key, value in results.items():
    print(f"{key}: {value} seconds")

