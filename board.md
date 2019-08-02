Partner A Q-1


new merge sort
takes a proc
shouldnt modify and return new sorted array
method for class array

[].merge_sort = []


[1,2,3,4].merge_sort
class Array
    def merge_sort(&prc)
        return self.dup if self.length <= 1
        prc ||= Proc.new {|a, b| a <=> b}

        half = self.length / 2
        left = self.take(half)
        right = self.drop(half)
        sorted_left = left.merge_sort(&prc)
        sorted_right = right.merge_sort(&prc)

        Array.merge(sorted_left, sorted_right, &prc)
    end

    def self.merge(left, right, &prc)
        sorted = []
        until left.empty? || right.empty?
            if prc.call(left.first, right.first) == -1
                sorted << left.shift
            else
                sorted << right.shift
            end
        end

        sorted + left + right
    end
end

b <=> a

_____________________________________________________________________________

Partner A Q -2

## Monkey Patching

### my_flatten

Write a method that flattens an array to the specified level. If no level
is specified, it should entirely flatten nested arrays.

Examples:

```ruby
# Without an argument:
[["a"], "b", ["c", "d", ["e"]]].my_flatten = ["a", "b", "c", "d", "e"]

# When given 1 as an argument:
# (Flattens the first level of nested arrays but no deeper)
[["a"], "b", ["c", "d", ["e"]]].my_flatten(1) = ["a", "b", "c", "d", ["e"]]
```

class Array
    def my_flatten(level=nil)
        duped_array = self.dup

        if level == nil
            until duped_array.none? {|ele| ele.is_a?(Array)}
                duped_array.each_with_index do |ele, idx|
                    if ele.is_a?(Array)
                        current_array = ele.dup
                        duped_array.delete_at(idx)
                        duped_array.insert(idx, ***current_array)
                    end
                end
            end

            return duped_array
        end

current_array = ***[3,4] = 3,4
        until level.times do
            idx = 0
            while idx < dupe_array.length
                if ele.is_a?(Array)
                    current_array = ele.dup
                    duped_array.delete_at(idx)
                    duped_array.insert(idx, ***current_array)
                end

                idx += 1
            end
        end
        return duped_array
    end
end

_____________________________________________________________________________

Partner B Q-1






binary searach 

binary_search([1,2,3,4,5], 1)

def binary_search(arr, key)
hlf = arr.length / 2
ele_hlf = arr[hlf]


case key <=> ele_hlf
when == 0
    return hlf if ele_hlf == key
when == -1
    left = arr[0...hlf]
    binary_search(left, key)
when == 1
    right = arr[(hlf + 1)..-1]
    binary_searc(right, key) + (hlf + 1)
end

# binary_search([1,2,3,4,5], 5)
#right = [4,5]
#hlf = 2
#+ (hlf + 1)

#binary_searc([4,5], 5) 
#hlf = 1
#right_arr[1] == 5 which == key

#1 + 2 + 1
#arr[4] ==  5 which == key




end

# binary_search([1,2,3,4,5], 3) 
# hlf = 2
# arr[2] = 3 which is they key
#returns 2



# binary_search([1,2,3,4,5], 1)
#hlf = 1
#arr[hlf] = 2 != key
#arr [1]
#binary_search(arr, key)
#hlf = 0
#arr[0] = 1 which == key
#returns 1




________________________________________________________________
Partner B Q-2


Monkey_patch my each


class Array
    def my_each(&proc)
        idx = 0
        
        while idx < length
            prc.call(self[idx])
            idx +=1
        end
        self
    end
end