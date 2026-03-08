# Assignment 5
## Code
```C++
#include <iostream>
#include <vector>
#include <list>
#include <string>
#include <utility>
#include <iomanip>
using namespace std;
//Part 1 - implementing given hash class structure using linked lists
class HashTable {
private:
    // main table storage
    vector<list<pair<string, int>>> table;
    int currentSize;
    int capacity;
    int collisionCount;
//Part 2 - implementing given polynomial rolling hash
    int hashFunction(const string& key) const {
        const int prime = 31;
        long long hash = 0;

        for (char c : key) {
            hash = hash * prime + c;
        }

        return hash % capacity;
    }
//Part 4- rehash. double table size and re-insert all existing elements for high load factor
    void rehash() {
        vector<list<pair<string, int>>> oldTable = table; //save old table

        capacity = capacity * 2; //double table size
        table.clear(); //clear table and make bigger one
        table.resize(capacity);
        //start at zero again for new table
        currentSize = 0;
        collisionCount = 0;
        //put all the old stuff into the new table
        for (auto bucket: oldTable) {
            for (auto item : bucket) {
                insert(item.first, item.second);
            }
        }
    }

public:
    //hash table contsructor with default starting values
    HashTable(int size = 11) {
        capacity = size;
        currentSize = 0;
        collisionCount = 0;
        table.resize(capacity);
    }
//Part 3 - Insert and collision handling. Check if key exists, update if it does intead of duplicating
    void insert(const string& key, int value) {
        int index = hashFunction(key); //find the right bucket for key
        //check if key is in bucket, if it is, update and return
        for (auto& item: table[index]) {
            if (item.first == key) {
                item.second = value;
                return;
            }
        }
        // count collisions due to bucket not being empty for an insertion
        if (!table[index].empty()) {
            collisionCount++;
        }
        // add new value to bucket
        table[index].push_back({key, value});
        currentSize++;
        // resize table to increase efficiency when table gets too full
        if (loadFactor() > 0.75) {
            rehash();
        }
    }
// Part 5 - remove and test
    bool remove (const string& key) {
        int index = hashFunction(key); //find bucket for key
        //search bucket
        for (auto it = table[index].begin(); it != table[index].end(); ++it) {
            if (it->first == key) {
                table[index].erase(it); //remove matching value
                currentSize--;
                return true;
            }
        }

        return false;
    }
//Part 5 search
    int search(const string& key) const {
        int index = hashFunction(key); //find bucket for key
        //search bucket for key
        for (auto item : table[index]) {
            if (item.first == key) {
                return item.second;
            }
        }

        return -1;
    }
//Part 4 - load factor, calculates and returns load factor to determine whether rehash is needed
    double loadFactor() const {
        return (double) currentSize / capacity;
    }
    // returns number of elements currently stored
    int size() const {
        return currentSize;
    }
    // returns true if the table is empty
    bool isEmpty() const {
        return currentSize == 0;
    }
    //print the contents of the table by bucket
    void printTable() const {
        for (int i = 0; i < capacity; i++) {
            cout << "bucket" << i << ": ";

            for (auto item : table[i]) {
                cout << "(" << item.first << "," << item.second << ") ";
            }

            cout << endl;
        }
    }
// Part 5/6 - functions to get capacity, collisions, bucket size
    int getCollisionCount() const {
        return collisionCount;
    }

    int getCapacity() const {
        return capacity;
    }

    int getMaxBucketSize() const {
        int maxSize = 0;
        // find biggest bucket, assign to maxSize
        for (auto bucket : table) {
            if (bucket.size() > maxSize) {
                maxSize = bucket.size();
            }
        }

        return maxSize;
    }
//Part 6 - Experimental analysis
    double getAverageBucketLength() const {
        int usedBuckets = 0;
        int totalItems = 0;
        // count how many buckets aren't empty and how many items inside
        for (auto bucket : table) {
            if (!bucket.empty()) {
                usedBuckets++;
                totalItems += bucket.size();
            }
        }
        // don't divide by zero
        if (usedBuckets == 0) {
            return 0;
        }

        return (double) totalItems / usedBuckets;
    }
};
// This function runs all the helper functions to get stats for the hash table
void runTest(string arr[], int n, string label) {
    HashTable ht;
    //insert all strings from array into hash table
    for (int i = 0; i < n; i++) {
        ht.insert(arr[i], i);
    }

    cout << "\n=== " << label << " ===" << endl;
    cout << "Table capacity: " << ht.getCapacity() << endl;
    cout << "Number of elements: " << ht.size() << endl;
    cout << "load factor: " << fixed << setprecision(2) << ht.loadFactor() << endl;
    cout << "total collisions: " << ht.getCollisionCount() << endl;
    cout << "Max bucket size: " << ht.getMaxBucketSize() << endl;
    cout << "Average bucket length: " << ht.getAverageBucketLength() << endl;
}
//Part 5 - testing program
// insert 100 words into a hash table
int main() {
    const int N = 100;
    // come up with 100 random words and type them here for the array
    string randomStrings[N] = {
        "xj3k", "panda", "moon7", "alpha", "zebra", "delta9", "kiwi", "raven", "mango", "cable",
        "tiger", "jelly", "stone", "apple1", "grape", "cloud", "chair", "plant", "mouse", "river",
        "ocean", "brick", "flame", "shark", "beach", "house", "train", "dream", "green", "brown",
        "light", "pizza", "toast", "storm", "glass", "piano", "drums", "bread", "clock", "snake",
        "paper", "queen", "robot", "juice", "laugh", "track", "vivid", "watch", "zesty", "lemon",
        "spice", "whale", "table", "crown", "eagle", "frame", "ghost", "honey", "ivory", "jacket",
        "kernel", "ladder", "magnet", "needle", "orange", "pepper", "quartz", "rocket", "silver", "thunder",
        "unicorn", "violet", "window", "yellow", "anchor", "basket", "circle", "dragon", "engine", "forest",
        "guitar", "hammer", "island", "jungle", "kitten", "lantern", "mirror", "napkin", "orchid", "parrot",
        "quiver", "rainbow", "saddle", "temple", "umpire", "valley", "wizard", "yogurt", "zenith", "button"
    };

    // two other types of keys
    string sequentialKeys[N];
    string samePrefixKeys[N];
    // build same and sequential keys
    for (int i = 0; i < N; i++) {
        sequentialKeys[i] = "student" + to_string(i + 1);

        if (i < 10) {
            samePrefixKeys[i] = "data_000" + to_string(i);
        }
        else {
            samePrefixKeys[i] = "data_00" + to_string(i);
        }
    }
    // hash table for testing in part 5
    HashTable ht;
    // insert 100 random words
    for (int i = 0; i < N; i++) {
        ht.insert(randomStrings[i], i + 100);
    }
    // print out all the required stats
    cout << "TEST" << endl;
    cout << "Table capacity: " << ht.getCapacity() << endl;
    cout << "Number of elements: " << ht.size() << endl;
    cout << "load factor: " << fixed << setprecision(2) << ht.loadFactor() << endl;
    cout << "Total collisions: " << ht.getCollisionCount() << endl;
    // search for an existing value and a non existing value
    cout << "\nSearch tests:" << endl;
    cout << "Searching for panda: " << ht.search("panda") << endl;
    cout << "searching for supercalifragilisticexpialidocious: " << ht.search("supercalifragilisticexpialidocious") << endl;
    // remove a couple of items and verify via search they are in fact removed
    cout << "\nRemove tests:" << endl;
    cout << "removing panda: " << (ht.remove("panda") ? "Success" : "Failure") << endl;
    cout << "searching for panda again: " << ht.search("panda") << endl;
    cout << "Removing ghost: " << (ht.remove("ghost") ? "Success" : "Failure") << endl;
    cout << "Searching for ghost again: " << ht.search("ghost") << endl;
    // run all the tests for each type of data 
    runTest(randomStrings, N, "Random Strings");
    runTest(sequentialKeys, N, "Sequential Keys");
    runTest(samePrefixKeys, N, "Same Prefix Keys");

    return 0;
}
```
## Written Analysis
Prior to implementing these methods, I expected random to produce the fewest collisions, bucket size, and average length. I found that my random ended up with the highest collisions, and my sequential and prefix produced zero collisions in the final table with the shortest length and smallest bucket size. This was concerning to me as these were not the expected results. After further research, I noticed a couple of things. First, we were instructed to insert 100 words. Since words are not really truly random, not like an alphanumeric random string generator, this could result in more collisions than expected. Secondly, we were tasked with resetting the collision counter where appropriate. I took this to mean between rehashings. This results in the sequential and prefix ending up with zero collisions on their final table, as seemingly every value found it's own bucket at the end. 

I wanted to see what would happen if I approched both of these things differently. First, I replaced my 100 words with a random string generator. Second, I added a cumulative total collision counter to my code. Third, our prefix values ended up being identical to sequential, so I changed the prefix to repeated a's to get more collisions. The result of these changes is that my random did reduce collisions, bucket, and length size, but it was still higher than the others. My prefix, with the changes, also separated itself from sequential with more collisions. I still wasn't satisfied with the random results, so after more research, I determined that the starting size of 11 was relatively small. By increasing the hash table size from 11 to 150, then to 1100, and then to 11000, I could see a trend where random would remain the highest of the three until all three types leveled out to basically zero. This suggests that logically, my hash logic is functioning as expected, but for whatever reason this set of data and hash algorithm produces slightly unusual results. 

These obserations are still mostly consistent with expectations. When load factor is high, collisions are more likely because of sharing limited buckets. As the table capacity increases, load factor goes down and the probability of collisions goes down. Once we removed the table size limit, even varied datasets start to resemble uniform hashing which explains why all three datasets produced virtually identical results when the initial size was set to 11000.
```C++
#include <iostream>
#include <vector>
#include <list>
#include <string>
#include <utility>
#include <iomanip>
#include <random>
using namespace std;

// helper function to generate random alphanumeric strings
string randomString(int length) {
    const string chars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    static random_device rd;
    static mt19937 gen(rd());
    uniform_int_distribution<> dist(0, chars.size() - 1);

    string s = "";
    for (int i = 0; i < length; i++) {
        s += chars[dist(gen)];
    }

    return s;
}

//Part 1 - implementing given hash class structure using linked lists
class HashTable {
private:
    // main table storage
    vector<list<pair<string, int>>> table;
    int currentSize;
    int capacity;
    int collisionCount;
    int totalCollisionCount;

    //Part 2 - implementing given polynomial rolling hash
    int hashFunction(const string& key) const {
        const int prime = 31;
        long long hash = 0;

        for (char c : key) {
            hash = hash * prime + c;
        }

        return hash % capacity;
    }

    //Part 4- rehash. double table size and re-insert all existing elements for high load factor
    void rehash() {
        vector<list<pair<string, int>>> oldTable = table; //save old table

        capacity = capacity * 2; //double table size
        table.clear(); //clear table and make bigger one
        table.resize(capacity);

        //start at zero again for new table
        currentSize = 0;
        collisionCount = 0;

        //put all the old stuff into the new table
        for (auto bucket: oldTable) {
            for (auto item : bucket) {
                insert(item.first, item.second);
            }
        }
    }

public:
    //hash table constructor with default starting values
    HashTable(int size = 150) {
        capacity = size;
        currentSize = 0;
        collisionCount = 0;
        totalCollisionCount = 0;
        table.resize(capacity);
    }

    //Part 3 - Insert and collision handling. Check if key exists, update if it does intead of duplicating
    void insert(const string& key, int value) {
        int index = hashFunction(key); //find the right bucket for key

        //check if key is in bucket, if it is, update and return
        for (auto& item: table[index]) {
            if (item.first == key) {
                item.second = value;
                return;
            }
        }

        // count collisions due to bucket not being empty for an insertion
        if (!table[index].empty()) {
            collisionCount++;
            totalCollisionCount++;
        }

        // add new value to bucket
        table[index].push_back({key, value});
        currentSize++;

        // resize table to increase efficiency when table gets too full
        if (loadFactor() > 0.75) {
            rehash();
        }
    }

    // Part 5 - remove and test
    bool remove (const string& key) {
        int index = hashFunction(key); //find bucket for key

        //search bucket
        for (auto it = table[index].begin(); it != table[index].end(); ++it) {
            if (it->first == key) {
                table[index].erase(it); //remove matching value
                currentSize--;
                return true;
            }
        }

        return false;
    }

    //Part 5 search
    int search(const string& key) const {
        int index = hashFunction(key); //find bucket for key

        //search bucket for key
        for (auto item : table[index]) {
            if (item.first == key) {
                return item.second;
            }
        }

        return -1;
    }

    //Part 4 - load factor, calculates and returns load factor to determine whether rehash is needed
    double loadFactor() const {
        return (double) currentSize / capacity;
    }

    // returns number of elements currently stored
    int size() const {
        return currentSize;
    }

    // returns true if the table is empty
    bool isEmpty() const {
        return currentSize == 0;
    }

    //print the contents of the table by bucket
    void printTable() const {
        for (int i = 0; i < capacity; i++) {
            cout << "bucket" << i << ": ";

            for (auto item : table[i]) {
                cout << "(" << item.first << "," << item.second << ") ";
            }

            cout << endl;
        }
    }

    // Part 5/6 - functions to get capacity, collisions, bucket size
    int getCollisionCount() const {
        return collisionCount;
    }

    int getTotalCollisionCount() const {
        return totalCollisionCount;
    }

    int getCapacity() const {
        return capacity;
    }

    int getMaxBucketSize() const {
        int maxSize = 0;

        // find biggest bucket, assign to maxSize
        for (auto bucket : table) {
            if (bucket.size() > maxSize) {
                maxSize = bucket.size();
            }
        }

        return maxSize;
    }

    //Part 6 - Experimental analysis
    double getAverageBucketLength() const {
        int usedBuckets = 0;
        int totalItems = 0;

        // count how many buckets aren't empty and how many items inside
        for (auto bucket : table) {
            if (!bucket.empty()) {
                usedBuckets++;
                totalItems += bucket.size();
            }
        }

        // don't divide by zero
        if (usedBuckets == 0) {
            return 0;
        }

        return (double) totalItems / usedBuckets;
    }
};

// This function runs all the helper functions to get stats for the hash table
void runTest(string arr[], int n, string label) {
    HashTable ht;

    //insert all strings from array into hash table
    for (int i = 0; i < n; i++) {
        ht.insert(arr[i], i);
    }

    cout << "\n=== " << label << " ===" << endl;
    cout << "Table capacity: " << ht.getCapacity() << endl;
    cout << "Number of elements: " << ht.size() << endl;
    cout << "load factor: " << fixed << setprecision(2) << ht.loadFactor() << endl;
    cout << "final table collisions: " << ht.getCollisionCount() << endl;
    cout << "total collisions overall: " << ht.getTotalCollisionCount() << endl;
    cout << "Max bucket size: " << ht.getMaxBucketSize() << endl;
    cout << "Average bucket length: " << ht.getAverageBucketLength() << endl;
}

//Part 5 - testing program
// insert 100 words into a hash table
int main() {
    const int N = 100;

    string randomStrings[N];

    // generate 100 random strings
    for (int i = 1; i < N; i++) {
        randomStrings[i] = randomString(8);
    }

    // two other types of keys
    string sequentialKeys[N];
    string samePrefixKeys[N];

    // build same and sequential keys
    for (int i = 0; i < N; i++) {
        sequentialKeys[i] = "student" + to_string(i + 1);

        samePrefixKeys[i] = "aaaaaaaaa" + to_string(i);
    }

    // hash table for testing in part 5
    HashTable ht;

    // insert 100 random words
    for (int i = 0; i < N; i++) {
        ht.insert(randomStrings[i], i + 100);
    }

    // print out all the required stats
    cout << "TEST" << endl;
    cout << "Table capacity: " << ht.getCapacity() << endl;
    cout << "Number of elements: " << ht.size() << endl;
    cout << "load factor: " << fixed << setprecision(2) << ht.loadFactor() << endl;
    cout << "Final table collisions: " << ht.getCollisionCount() << endl;
    cout << "Total collisions overall: " << ht.getTotalCollisionCount() << endl;

    // search for an existing value and a non existing value
    cout << "\nSearch tests:" << endl;
    cout << "Searching for panda: " << ht.search("panda") << endl;
    cout << "searching for supercalifragilisticexpialidocious: " << ht.search("supercalifragilisticexpialidocious") << endl;

    // remove a couple of items and verify via search they are in fact removed
    cout << "\nRemove tests:" << endl;
    cout << "removing panda: " << (ht.remove("panda") ? "Success" : "Failure") << endl;
    cout << "searching for panda again: " << ht.search("panda") << endl;
    cout << "Removing ghost: " << (ht.remove("ghost") ? "Success" : "Failure") << endl;
    cout << "Searching for ghost again: " << ht.search("ghost") << endl;

    // run all the tests for each type of data
    runTest(randomStrings, N, "Random Strings");
    runTest(sequentialKeys, N, "Sequential Keys");
    runTest(samePrefixKeys, N, "Same Prefix Keys");

    return 0;
}
```
