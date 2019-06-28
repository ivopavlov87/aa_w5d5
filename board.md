
```rb
class Array

    def merge_sort(array, &prc)
        prc ||= Proc.new { |a, b| a <=> b }
        return [] if length == 0
        return self if length == 1

        middle = self.length / 2

        left = self.take(middle)
        right = self.drop(middle)

        sorted_left = merge_sort(left, &prc)
        sorted_right = merge_sort(right, &prc)

        merge(sorted_left, sorted_right, &prc)
    end

    def merge(arr1, arr2, &prc)
        # if arr1.empty?
        #     return arr2
        # elsif arr2.empty?
        #     return arr1
        # end
        sorted = []
        until arr1.empty? || arr2.empty?
            if prc.call(arr1[0], arr2[0]) == -1
                sorted << arr1.shift
            else
                sorted << arr2.shift
            end
        end
        sorted + arr1 + arr2
    end
end


def bsearch(array, target)
    return nil if array.empty?

    mid_idx = array.length / 2
    if array[mid_idx] == target 
        return mid_idx 
    elsif array[mid_idx] > target 
        bsearch(array.take(mid_idx))
    else
        res = bsearch(array.drop(mid_idx + 1))
        if res.nil?
            return nil 
        else       
            mid_idx + 1 + res 
        end 
    end
end 

# ```ruby
# # Without an argument:
# [["a"], "b", ["c", "d", ["e"]]].my_flatten = ["a", "b", "c", "d", "e"]

# # When given 1 as an argument:
# # (Flattens the first level of nested arrays but no deeper)
# [["a"], "b", ["c", "d", ["e"]]].my_flatten(1) = ["a", "b", "c", "d", ["e"]]
# ```
class Array

    def my_flatten(level = nil)
    result = []

        if level.nil?
            self.each do |ele|
                if ele.is_a?(Array)
                    result += ele.my_flatten
                else
                    result << ele
                end
            end
        else
            return self if level < 1

            self.each do |ele|
                if ele.is_a?(Array)
                    result += ele.my_flatten(level - 1)
                else
                    result << ele
                end
            end
        end
        result
    end
end

# 4322 => 11 => 2


2 + digi_root(432)
          2         + digi_root(43)
                            3        + digi_root(4)
                                            4

                                            dig11
def digi_root(num)
    return num if num < 10

    result = num % 10 + digi_root(num / 10)
    digi_root(result)
end


def jumbo_sort(string, alphabet)
    alphabet ||= ("a".."z").to_a
   sorted = string.split("").sort_by {|ele| alphabet.index(ele)}
   sorted.join("") 
end 


# my_reduce

# Write an array method that calls the given block on each element and
# combines each result one-by-one with a given accumulator. If no accumulator
# is given, the first element is used.
class Array
    def my_reduce(acc = nil, &prc)
        accumulator ||= self.shift
        prc ||= Proc.new { |acc, ele| acc + ele }

        self.each do |ele|
            acc = prc.call(acc, ele)
        end

        acc
    end
end

### dups

# Write an array method that returns a hash where the keys are any element
# that appears in the array more than once, and the values are sorted arrays
# of indices for those elements.
class Array 
    def dups
        hash = Hash.new {|h, k| h[k] = []}
        self.each_with_index do |ele, idx|
            hash[ele] << idx 
        end 
        hash.select {|k,v| v.length > 1}
    end
end 

### Shuffled Sentences

# This method returns true if the words in the string can be rearranged to form the
# sentence passed as an argument. Words are separated by spaces.

Example:

# ```ruby
# "cats are cool".shuffled_sentence_detector("dogs are cool") => false
# "cool cats are".shuffled_sentence_detector("cats are cool") => true
class String
    def shuffled_sentence_detector(string)
        org_words = self.split(" ")
        words = string.split(" ")
        org_words.each do |word|
            return false unless string.include?(word)
        end

        words.each do |word|
            return false unless self.include?(word)
        end

        true
    end
end

# Write a method that returns the largest prime factor of a number.
# We recommend writing a `is_prime?` helper method.
def is_prime?(num)
    (2...num).none? {|el| num % ele == 0}
end  

def largest_prime(num)
    num.downto(2).each do |i|
        if num % i == 0 && is_prime?(i)
            return i
        end   
    end 
    return nil  
end   

### Fibonacci

# Write a method that finds the first `n` Fibonacci numbers recursively.


def fib(n)
    return [] if n == 0
    return [0] if n == 1
    return [0, 1] if n == 2

    seq = fib(n - 1)
    seq << seq[-1] + seq[-2]
end


# Write a method that recursively finds the first `n` factorial numbers
# and returns them. N! is the product of the numbers 1 to N.
# Be aware that the first factorial number is 0!, which is defined
# to equal 1. The 2nd factorial is 1!, the 3rd factorial is 2!, etc.

def factorial_rec(n)
    return [1,1] if n == 2 
    factorial_rec(n-1) << factorial(n)
end

def factorial(n)
    return 1 if n == 1 || 2 
    (n-1) * factorial(n-1)
end     

def factorials_rec(num)
  if num == 1
    [1]
  else
    facs = factorials_rec(num - 1)
    facs << facs.last * (num - 1)
    facs
  end
end

def factorials_rec(num)
    return [1] if num == 1

  arr = factorials_rec(num-1)
  arr << (num - 1) * arr.last
  arr
end
```