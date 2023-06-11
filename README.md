# The Hospital Drone Scheduler

A Hospital Done **Nest** delivers many types of products to many hospitals using a fleet of **Zips**, which are basically autonomous flight drones. In order to provide the best experience to our customers, we want to minimize the time-to-deliver. That said, some of our orders are **Emergency** deliveries, which have the potential to be lifesaving, whereas other orders are **Resupply** deliveries, leaving us some flexibility in delivery time.

The reality is that we have a limited number of Zips, and so we need to be more clever than immediately sending out a Zip as each order comes in. To help manage these logistics, the purpose of this exercise will be to write a `ZipScheduler` utility, to determine when and to which hospitals we should send out Zips for delivery.

To make things more interesting, we will also allow each Zip to carry multiple packages at a time. This means that a Zip can take off and deliver to several hospitals on one trip, before flying back to the Nest. Zips are limited by the cumulative distance they can fly on a given trip and have a maximum number of packages they can carry.

## Inputs

The starter code is set up to read these files which live in the `inputs` directory:

### `hospitals.csv`
The locations of the hospitals we are delivering to are provided in a CSV file specifying:

`Hospital Name, North, East`

`North` and `East` are provided in **meters** with our operations center assumed to be at `(0,0)`.

### `orders.csv`
In general operations, we will receive a sequence of orders in real-time. Each order specifies the hospital the delivery needs to go to, and the priority of the delivery. To test your system we are providing a list of orders in a CSV, specified as:

`Received Time, Hospital Name, Priority`

`Received Time` will be specified in seconds-since-midnight, and priority will be either `Emergency` or `Resupply`.

## Assumptions

1. You may assume that the Zip flies a series of straight-line paths, starting at the Nest, passing through each hospital, and then returning to the Nest.
2. The total length of the cumulative path cannot be greater than the maximum range of the Zip (defined in the starter code).
3. Zips travel at a fixed flight speed (also defined in the starter code).
4. Zips can only take off with up to the maximum number of packages (also defined in the starter code).
5. Once they have returned, Zips charge instantly and can be immediately sent out again.
6. The Nest has a limited number of Zips (also defined in the starter code).

## What We're Looking For
### 1. Implement the Scheduler

The primary deliverable is a simple implementation of a `ZipScheduler` class, which can be used as part of our delivery management system. We've started this class, and ask that you fill in the following APIs:

`queue_order(order)` is used to add a new order to our queue, and will be called every time a new order arrives.

`launch_flights(current_time)` will be called periodically (e.g. once a minute), and should return a list of flights that are launched right now, with each flight having an ordered list of orders to serve. All flights returned from this will be launched simultaneously.