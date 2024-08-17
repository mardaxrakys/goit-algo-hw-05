def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    iterations = 0

    while low <= high:
        mid = (low + high) // 2
        iterations += 1
        if arr[mid] == target:
            return (iterations, arr[mid])
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    
    # Повертаємо кількість ітерацій і найменший елемент, більший або рівний заданому значенню
    # Якщо все ж не знайшли жодного елемента >= target, то повернемо None
    if low < len(arr):
        return (iterations, arr[low])
    else:
        return (iterations, None)

# Приклад використання
arr = [1.1, 2.2, 3.3, 4.4, 5.5]
target = 3.0
print(binary_search(arr, target))
