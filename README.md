# Cost-estimation-tool-for-mechanical-parts-
# ==========================================
# Project Title: 
# Python-Based Cost Estimation Tool 
# for Mechanical Components using OOP
# ==========================================
# Base class for part
class Part:
 def __init__(self, name, quantity):
 self.name = name 
 self.quantity = quantity 
# Material cost class
class MaterialCost:
 def __init__(self, price_per_kg, weight_kg):
 self.price_per_kg = price_per_kg 
 self.weight_kg = weight_kg 
 def compute(self):
 return self.price_per_kg * self.weight_kg 
# Machining cost class
class MachiningCost:
 def __init__(self, rate_per_hour, time_min, tooling_cost=0):
 self.rate_per_hour = rate_per_hour 
 self.time_min = time_min 
 self.tooling_cost = tooling_cost 
 def compute(self):
 return self.rate_per_hour * (self.time_min / 60) +
self.tooling_cost 
# Labor cost class
class LaborCost:
 def __init__(self, rate_per_hour, time_min):
 self.rate_per_hour = rate_per_hour 
 self.time_min = time_min 
 def compute(self):
 return self.rate_per_hour * (self.time_min / 60)
# Energy cost class
class EnergyCost:
 def __init__(self, power_kw, rate_per_kwh, time_min):
 self.power_kw = power_kw 
 self.rate_per_kwh = rate_per_kwh 
 self.time_min = time_min 
 def compute(self):
 return self.power_kw * self.rate_per_kwh * (self.time_min / 60)
# Overhead cost class
class Overhead:
 def __init__(self, percent):
 self.percent = percent 
 def compute(self, subtotal):
 return subtotal * (self.percent / 100)
# Cost Estimator class
class CostEstimator:
 def __init__(self, part, material, machining, labor, energy, overhead):
 self.part = part 
 self.material = material 
 self.machining = machining 
 self.labor = labor 
 self.energy = energy 
 self.overhead = overhead 
 def total_cost(self):
 m1 = self.material.compute()
 m2 = self.machining.compute()
 m3 = self.labor.compute()
 m4 = self.energy.compute()
 subtotal = m1 + m2 + m3 + m4 
 overhead_cost = self.overhead.compute(subtotal)
 total_unit = subtotal + overhead_cost 
 total_job = total_unit * self.part.quantity 
 # return dictionary of costs
 return {
 'Material': m1, 'Machining': m2, 'Labor': m3,
 'Energy': m4, 'Overhead': overhead_cost,
 'Total/unit': total_unit, 'Total/job': total_job # ==========================================
# MAIN PROGRAM
# ==========================================
if __name__ == "__main__":
 print("=== COST ESTIMATION TOOL ===")
 # Define part and cost parameters
 part = Part("Shaft", 10)
 material = MaterialCost(80, 1.5)
 machining = MachiningCost(400, 45, 20)
 labor = LaborCost(150, 20)
 energy = EnergyCost(2, 10, 45)
 overhead = Overhead(12.5)
 # Compute and display result
 cost = CostEstimator(part, material, machining, labor, energy,
overhead)
 result = cost.total_cost()
 print("\n--- COST BREAKDOWN ---")
 for k, v in result.items():
 if "Total" in k:
 print(f"{k}: ₹{v:.2f}")
 else:
 print(f"{k} Cost: ₹{v:.2f}")
 print("===========================")
