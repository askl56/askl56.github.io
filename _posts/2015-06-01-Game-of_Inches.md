---
layout: post
title: Game of Inches
description: "Comments on programming for beginners"
tags: [coding, ruby, python, javascript]
image:
  background: triangular.png
---

Although still a veritable spring chicken in the coding world and beyond, I am beginning to grow feathers.

This post will no doubt bore any veterans to the core, but it relays something which I found incredibly interesting. When learning to code, I feel that I have gone through three distinct phases. The first was learning anything and everything I could to be able to churn out code as quickly as possible. This "devil may care" attitude serves its own purpose in the beginning, but like with any science, one quickly realises that the devils are everywhere in the details. Writing code is easy. Fixing, testing and refactoring it are not.

The second phase that I went through was when suddenly I realised that testing was important. For many programmers, I'm sure testing is boring as shit. It demands as much code, if not more than what it is testing, and it somewhat inhibits the flow of whatever one is trying to do. These are the attacks usually laid at the door of TDD and BDD. Whilst I recognise that there is undoubtedly some truth in them, it is much clearer to me that tests are vital and can even be fun. For some reason I have managed to get myself hooked on the dopamine release of having a fully working RSpec suite, with a deluge of green dots. I'm not entirely sure how or why this has happened, but I am definitely glad that it has.

The third phase began as I started looking for jobs. I had never really looked at code as art before, nor given the comparison a lot of thought. However, as I looked at the code of others and compared it with my own, I was struck by how stark the difference is. In his excellent book, [Eloquent Ruby](http://www.amazon.co.uk/Eloquent-Ruby-Addison-Wesley-Professional/dp/0321584104), Russ Olsen describes for the first time, the game of inches. Good code should be a narrative, which not only works, but should require no explanation. Those two parts are equally important.

Let me give you an example. I was working on a Prime multiplication table calculator for the command line. You can find my finished product [here](https://github.com/askl56/PrimeTime). In essence, the program had to calculate, without the use of the Prime library in Ruby, a list of primes provided by the user in the form of n, then multiply them together. I do not wish to write a thesis on this so I will focus simply on the code which finds the prime numbers and stores them in an array.

In my first iteration, I had this:

{% highlight ruby linenos %}

# Firstly a function to determine if a given number is Prime.

def prime?(n)
  (2..n - 1).to_a.all? { |num| n % num != 0 }
end

# Secondly store the prime numbers in an array.

def prime_storage(n)
  prime_array = []
  count = 2
  while prime_array.length < n
    prime_array << (count) if prime?(count)
    count += 1
  end
  prime_array
end

{% endhighlight %}

For a beginner, this code isn't bad. It does the job at hand, it tests each number to see if it is prime and if it is then it stores them in the array and increments the count until the count reaches the number provided by the user.

However, I wasn't happy. When looking at it, it simply appeared bulky, and frankly unpleasant, at least from an aesthetic point of view. It is also inefficient mathematically since it has to continuously compute through every number to n checking if its prime. By complete chance, and reading an unrelated Ruby article, I stumbled across the Lazy emunerator. After messing around for nearly a day, I came up with this:

{% highlight ruby linenos %}

def find_primes(n)
  inf = Float::INFINITY

  primes = (2..inf).lazy.select do |i|
    (2...i).none? {|x| i % x == 0  }
  end

  primes.first(n)
end

{% endhighlight %}

I'm not claiming it's perfect, but it's a whole hell of a lot cleaner than the first version, and far more to the point, I have managed to fit two different methods into one. There is something immensely satisfying about learning more and more about code design and how things are meant to be. For me certainly, writing better designed code has been a massive contributor to my confidence in terms of coding, and it undoubtedly has helped to reinforce the feeling that I love, namely that a piece of code is never finished and can always be improved upon.
