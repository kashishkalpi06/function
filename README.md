from datetime import datetime

class CarModel:
    def __init__(self, name):
        self.name = name
        self.parts = []

    def add_part(self, part):
        self.parts.append(part)

class CarPart:
    def __init__(self, name, model):
        self.name = name
        self.model = model
        self.service_criteria = []

    def add_service_criteria(self, criteria):
        self.service_criteria.append(criteria)

    def needs_service(self, tire_wear_array):
        if self.name == "Carrigan Tire":
            # Carrigan tires should be serviced if any tire's wear is greater than or equal to 0.9
            return any(wear >= 0.9 for wear in tire_wear_array)
        elif self.name == "Octoprime Tire":
            # Octoprime tires should be serviced if the sum of all tire wears is greater than or equal to 3
            return sum(tire_wear_array) >= 3
        else:
            return False  # For other parts, no servicing needed

class ServiceCriteria:
    def __init__(self, description, interval, part_type):
        self.description = description
        self.interval = interval
        self.part_type = part_type

class Service:
    def __init__(self, service_date, car_model, car_part, service_criteria):
        self.service_date = service_date
        self.car_model = car_model
        self.car_part = car_part
        self.service_criteria = service_criteria

class ServiceScheduler:
    def __init__(self):
        self.services = []

    def schedule_service(self, service):
        self.services.append(service)

    def get_upcoming_services(self):
        today = datetime.today()
        return [service for service in self.services if service.service_date >= today]

# Example usage:
car_model = CarModel("TestModel")
spindler_battery = CarPart("Battery", "Spindler Battery")

# Upgrade Spindler battery service criteria to 3 years
spindler_battery_criteria = ServiceCriteria("Check voltage", 3, "Battery")
spindler_battery.add_service_criteria(spindler_battery_criteria)

# Check tire servicing criteria
carrigan_tire = CarPart("Carrigan Tire", "Carrigan Tire")
octoprime_tire = CarPart("Octoprime Tire", "Octoprime Tire")

# Test tire servicing criteria
tire_wear_carrigan = [0.8, 0.95, 0.7, 0.85]
tire_wear_octoprime = [0.8, 0.9, 0.9, 0.4]

print(carrigan_tire.needs_service(tire_wear_carrigan))  # Should return True
print(octoprime_tire.needs_service(tire_wear_octoprime))  # Should return False
