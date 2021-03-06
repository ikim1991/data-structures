# Hash Tables  

### What are Hash Tables  

In Java they are referred to as Maps.  
In Python they are referred to as Dictionaries.  
In JavaScript they are referred to as Objects.  

A Hash Table stores a Key/Value pair into a data structure. The Key is used to generate the Hash through a Hash Function. The Hash is used as an index location in which to store the data. Each index location is known as a bucket. The buckets are organized in a static array.  
The Hash works as a memory address, which maps the Key to an index location. Both the Key/Value are then stored in one of the buckets.  
The use of Hash Functions and Hashes allows fast search and insertions in constant time, O(1), as the only computation required is to generate the Hash.  
The O(1) search time is the ideal scenario but there are instances where different keys can produce the same hash mapping to the same bucket. As we add more and more data, the likelihood of different keys sharing the same hash increases. This is known as Collision.  

When multiple keys share the same memory address, they are stored in another data structure known as Linked Lists. Linked Lists are similar to Arrays in a sense that it is ordered. This means the actual search time of the Hash Table becomes linear, O(n), due to collision. There are work arounds for collision but even without it, the time complexity is still improved compared to using an array as an alternative.  

### Hash Tables: Building a HashMap  

Java comes with a built-in HashMap class but the following Java code is a Hash Table built from scratch to demonstrate how a Hash Table uses a Hash Function to map the key to memory for storing data.  
[MyHashMap Class](./src/datastructures/hashtables/MyHashMap.java)  

```Java
public class MyHashMap {

    // Properties of the Hash Table, number of buckets/array size
    // Each bucket stores a Linked List of data in case of collision
    private int size;
    private LinkedList<String>[] buckets;

    public static void main(String[] args) {

        // Instantiating Hash Table with 10 buckets, 0 - 9 Index
        MyHashMap myHashTable = new MyHashMap(10);

        // Creating 10 keys to Hash and store into Hash Table
        String key1 = "Federer";
        String key2 = "Nadal";
        String key3 = "Djokovic";
        String key4 = "Thiem";
        String key5 = "Tsitipas";
        String key6 = "Monfils";
        String key7 = "Zverev";
        String key8 = "Raonic";
        String key9 = "Medvedev";
        String key10 = "Murray";

        // Storing Keys to Hash Table
        myHashTable.addKey(key1);
        myHashTable.addKey(key2);
        myHashTable.addKey(key3);
        myHashTable.addKey(key4);
        myHashTable.addKey(key5);
        myHashTable.addKey(key6);
        myHashTable.addKey(key7);
        myHashTable.addKey(key8);
        myHashTable.addKey(key9);
        myHashTable.addKey(key10);

        // Printing out the buckets and seeing where each data is stored
        for(LinkedList<String> key : myHashTable.buckets){
            System.out.print(key + "\t");
        }
        // Prints -> [Monfils, Raonic]	[Djokovic, Zverev]	[Tsitipas, Medvedev]	[Nadal]	null	[Federer, Thiem]	[Murray]	null	null	null
        // We see Collision for Indexes 0, 1, 2, 5
        // While Indexes 4, 7, 8, 9 have not been initialized
    }

    // Constructor for the Hash Table takes in an argument of the number of buckets
    // Creates an empty HashTable of defined size
    public MyHashMap(int size){
        this.size = size;
        this.buckets = new LinkedList[size];
    }

    // Method Hashes the Key and maps it to an index
    // the hashCode() method is a built in Java Hash Function
    // When the memory is not occupied, a Linked List is initialized and the data is stored.
    // When the memory is already occupied due to collision, the new data is linked
    // to the existing data through a linked list
    public void addKey(String key){
        int index = Math.abs(key.hashCode() % (size-1));
        System.out.println("Hash Function Generated index of: " + index);

        if(buckets[index] == null){
            buckets[index] = new LinkedList<String>();
        }

        System.out.println("Key: " + key + " was Added to index: " + index);
        buckets[index].add(key);
    }
}
```  

### When to Use Hash Tables  

##### Pros:  
  - Fast Lookups
  - Fast Insertion
  - Flexible Keys  

##### Cons:  
  - Unordered
  - Slow at Traversing
  - Space Complexity  
