# Introduction to Docker

## What is Docker?
A container platform that allows you to separate your application from the underlying infrastructure by bundling your code and all its dependencies to a self contained entity that will run the same on any supported system.

When it comes to software development, it's not the initial development that's challenging, it's everything that comes after that. Deploying code is a challenge, managing dependencies is a challenge, building rollbacks is a challenge, and all of these are made more challenging b/c development envs are seldom identical to production.

Docker containers are similar to their physical namesake. They allow you to take whatever software you need to run, bundle it up into a consistent format, and run it on any infrastructure that knows how to handle a container. The end result is like an executable for your code.

Can run apps on specific versions of containers. Having code run inside a container means is isolated from other processes and containers. Each container can have it's own process base, network stack, resource allocation, etc.

Docker containers are most often compared to virtual machines. They are completely different. Docker sits on top of VM, focuses more on application. Docker shares kernel w/ VM OS. 

## Docker Architecture