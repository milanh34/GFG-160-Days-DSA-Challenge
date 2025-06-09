<h1 align="center">🧠 LRU Cache 🧠</h1>

---

## 📝 Problem Statement

Design a data structure that implements a **Least Recently Used (LRU) Cache**. The cache should have:

- A fixed capacity `cap`.
- Ability to perform two types of queries:
  - `PUT x y`: Set the value `y` for key `x`.
  - `GET x`: Return the value of key `x` if it exists, otherwise return `-1`.

---

## 🚦 Function Definitions

### `int get(int key)`
- Returns the value if `key` is present in the cache.
- Moves the accessed key to the front (most recently used).
- Returns `-1` if not present.

### `void put(int key, int value)`
- If `key` is already present, update its value and move it to the front.
- If not present:
  - Add the key-value pair.
  - If the cache exceeds its capacity, remove the **least recently used** item.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
cap = 2, Q = 2, Queries = [["PUT", 1, 2], ["GET", 1]]
```

**Output:**  
```
[2]
```

**Explanation:**  
- Insert key `1` with value `2`.
- Get key `1` → returns `2`.

---

### ✅ Example 2:
**Input:**  
```
cap = 2, Q = 8, Queries = [
  ["PUT", 1, 2],
  ["PUT", 2, 3],
  ["PUT", 1, 5],
  ["PUT", 4, 5],
  ["PUT", 6, 7],
  ["GET", 4],
  ["PUT", 1, 2],
  ["GET", 3]
]
```

**Output:**  
```
[5, -1]
```

**Explanation:**
- After all operations, key `4` is accessed → returns `5`.
- Key `3` was never inserted or was evicted → returns `-1`.

---

## 🧠 Approach

- Use a **HashMap** to store key-value pairs for O(1) access.
- Use a **LinkedList** to maintain the order of usage:
  - The **front** of the list represents the **most recently used** item.
  - The **back** of the list represents the **least recently used** item.
- On every `get(key)`:
  - Return the value and move the key to the front.
- On every `put(key, value)`:
  - If key exists: update value and move to front.
  - If not:
    - If capacity is full, remove the last item (least recently used).
    - Add the new key-value and place the key at the front.

---

## ⏱️ Time and Space Complexity

| Complexity | Value     | Description                                  |
|------------|-----------|----------------------------------------------|
| Time       | O(1)      | For both `get` and `put` with LinkedHashMap  |
| Space      | O(cap)    | Space for storing `cap` elements              |

---

## 🎯 Constraints

- 1 ≤ `cap` ≤ 10³  
- 1 ≤ `Q` ≤ 10⁵  
- 1 ≤ `x`, `y` ≤ 10⁴  

---

## 💻 Code

```java
class LRUCache {
    
    static int cap;
    static LinkedList<Integer> list;
    static Map<Integer, Integer> map;

    LRUCache(int cap) {
        this.cap = cap;
        this.list = new LinkedList<>();
        this.map = new HashMap<>();
    }

    public static int get(int key) {
        if(!map.containsKey(key)){
            return -1;
        }
        list.remove(Integer.valueOf(key));
        list.addFirst(key);
        return map.get(key);
    }

    public static void put(int key, int value) {
        if(map.containsKey(key)){
            map.put(key, value);
            list.remove(Integer.valueOf(key));
        } else{
            if(map.size() >= cap){
                map.remove(list.removeLast());
            }
            map.put(key, value);
        }
        list.addFirst(key);
    }
}
```

---

> Made with ❤️ by Milan Haria
