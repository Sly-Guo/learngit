
# Leetcode day2  706.Design HashMap
## Problem description
Design a HashMap without using any built-in hash table libraries.
To be specific, your design should include these functions:
•	put(key, value) : Insert a (key, value) pair into the HashMap. If the value already exists in the HashMap, update the value.
•	get(key): Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key.
•	remove(key) : Remove the mapping for the value key if this map contains the mapping for the key.
__Note:__
•	All keys and values will be in the range of \\[0, 1000000](#).
•	The number of operations will be in the range of \\[1, 10000](#).
•	Please do not use the built-in HashMap library.

### C++:
	class MyHashMap {
	private:
		vector<int>vec;
	public:
		MyHashMap(){
			vec = vector<int>(1000001,-1);
		}
		void put(int key, int value)
		{
			vec[key] = value;
		}
		int get(int key)
		{
			return vec[key];
		}
		void remove(int key)
		{
			vec[key] = -1;
		}
	
	};
	
	/**
	 * Your MyHashMap object will be instantiated and called as such:
	 * MyHashMap* obj = new MyHashMap();
	 * obj->put(key,value);
	 * int param_2 = obj->get(key);
	 * obj->remove(key);
	 */*

### Python3:
	class MyHashMap:
	
	    def __init__(self):
	        """
	        Initialize your data structure here.
	        """
	        self.lst = [-1]*100001
	
	    def put(self, key: int, value: int) -> None:
	        """
	        value will always be non-negative.
	        """
	        self.lst[key] = value
	
	    def get(self, key: int) -> int:
	        """
	        Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key
	        """
	        return self.lst[key]
	
	    def remove(self, key: int) -> None:
	        """
	        Removes the mapping of the specified value key if this map contains a mapping for the key
	        """
	        self.lst[key] = -1
	
	
	# Your MyHashMap object will be instantiated and called as such:
	# obj = MyHashMap()
	# obj.put(key,value)
	# param_2 = obj.get(key)
	# obj.remove(key)