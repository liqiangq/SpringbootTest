# SpringbootTest
This is a simple full-stack web application that is a basic employee management application using React, Spring boot.

The main features:
-List Employee Functionality   
-Create Employee Functionality
-Update Employee Functionality

// get all employees
	@GetMapping("/employees")
	public List<Employee> getAllEmployees() {
		return employRepository.findAll();
	}

	// create employee rest api
	@PostMapping("/employees")
	public Employee createEmployee(@RequestBody Employee employee) {
		return employRepository.save(employee);
	}

	// get employee by id rest api
	@GetMapping("/employees/{id}")
	public ResponseEntity<Employee> getEmployeeById(@PathVariable Long id) {
		Employee employee = employRepository.findById(id)
				.orElseThrow(() -> new ResourceNotFoundException("Employee not exist with id:" + id));
		return ResponseEntity.ok(employee);
	}

	// update employee rest api
	@PutMapping("/employees/{id}")
	public ResponseEntity<Employee> updateEmployee(@PathVariable Long id, @RequestBody Employee employeeDetails) {
		Employee employee = employRepository.findById(id)
				.orElseThrow(() -> new ResourceNotFoundException("Employee not exist with id:" + id));

		employee.setFirstName(employeeDetails.getFirstName());
		employee.setLastName(employeeDetails.getLastName());
		employee.setEmailId(employeeDetails.getEmailId());

		Employee updateEmployee = employRepository.save(employee);
		return ResponseEntity.ok(employee);

	}
