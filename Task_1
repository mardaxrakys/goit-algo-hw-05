class HashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size

    def _hash_function(self, key):
        return hash(key) % self.size

    def insert(self, key, value):
        index = self._hash_function(key)
        if self.table[index] is None:
            self.table[index] = []
        for i, kv in enumerate(self.table[index]):
            k, v = kv
            if k == key:
                self.table[index][i] = (key, value)
                return
        self.table[index].append((key, value))

    def delete(self, key):
        index = self._hash_function(key)
        if self.table[index] is None:
            return  # Ключ не знайдено
        for i, kv in enumerate(self.table[index]):
            k, v = kv
            if k == key:
                del self.table[index][i]
                # Якщо після видалення список порожній, можемо очистити його
                if not self.table[index]:
                    self.table[index] = None
                return
