---
layout: post
title:  "Java Reactive"
date:   2022-01-24 22:00:00 +0700
categories: [java]
---

# Reactive Streams
- Provides standard for asynchronous stream, non-blocking applications.
- Use "Pull" model (Subscriber ask for data) instead of "Push" model (Publisher publish data)

## There are 4 interfaces
`Publisher<T>` -> provides bounb/unbound elements that publishing according to Sucscriber(s)
- void subscribe(Subscriber<? super T> s); : calls to subscribe to publisher, each call will start new Subscription.

`Processor<T, R>` -> be both Publisher and Sucscriber

`Subscriber<T>` ->
- void onSubscribe(Subscription s); : invoke after calling Publisher.subscribe
- void onNext(T t); : data sent by Publisher as request(one at a time)
- void onError(Throwable t);  to notifies errors and no more elements will be published
- void onComplete(); : to notifies all data sents and no more elements will be published

`Subscription` ->
- void request(long n); : request n elements from Publisher
- void cancel(); : inform Publisher to stop publishing data to this Subscription

# Java 9 Flow interfaces
Later, Java team includes Reactive Streams specification in to JDK, so calls Java 9 Flow interface


# Implementation of Reactive Streams
- RxJava
- Reactor
- Akka stream

# RxJava
- RxAndroid is an extension to RxJava
- Observable = `Publisher` imeplementation that emits 0..n elements
- There are also others types Flowable, Single, Maybe
- Disposable is subscription that we can use for cancellation

# Reactor
- Spring webflux is base of Reactor
- Cold stream = static, fix lenght stream of data. For example, harcoded Flux.just(...).
- Hot stream = dynamic, infinite stream of data. For example, data from Kafka.
- Mono = `Publisher` imeplementation that emits 0..1 elements
- Flux = `Publisher` imeplementation that emits 0..n elements
