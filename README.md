# AI-Route-optimization
traffic and transit management


import time
import random

class Vehicle:
    def __init__(self, vehicle_id, speed):
        self.vehicle_id = vehicle_id
        self.position = 0  # Position on the road segment
        self.speed = speed

    def move(self, traffic_light_state):
        if traffic_light_state == "green" or self.position < 5:  # Allow movement if green or before intersection
            self.position += self.speed
        else:
            # If red light and at the intersection, stop
            if self.position >= 5 and self.position < 10:
                pass # Vehicle waits at the light
            else:
                self.position += self.speed # Move if not at the intersection

class TrafficLight:
    def __init__(self, initial_state="red", cycle_time=10):
        self.state = initial_state
        self.cycle_time = cycle_time
        self.timer = 0

    def update(self):
        self.timer += 1
        if self.timer >= self.cycle_time:
            self.timer = 0
            if self.state == "red":
                self.state = "green"
            else:
                self.state = "red"

def run_simulation(duration=30, num_vehicles=5):
    vehicles = [Vehicle(f"Car_{i}", random.randint(1, 3)) for i in range(num_vehicles)]
    traffic_light = TrafficLight()

    print("Starting Real-time Traffic Simulation...")
    print("-" * 30)

    for t in range(duration):
        print(f"Time: {t}s")
        traffic_light.update()
        print(f"Traffic Light State: {traffic_light.state}")

        for vehicle in vehicles:
            vehicle.move(traffic_light.state)
            print(f"  {vehicle.vehicle_id} at position: {vehicle.position}")

        print("-" * 30)
        time.sleep(1) # Simulate real-time updates every second

if __name__ == "__main__":
    run_simulation()
