
#BodySense Use Cases


##Use Case: Identify Initial Occupancy Status of a Seat

###BriefDescription
The system identifies the initial occupancy status for airbag control.

###Precondition
The system has been initialized.

### 1.1 Basic Flow
1. The system requests weight from the SeatSensor.

2. INCLUDE USE CASE Self Diagnosis.

3. INCLUDE USE CASE Classify Occupancy Status.

4. The system VALIDATES THAT no error is detected.

5. The system SENDS the occupant class TO AirbagControlUnit.

Postcondition: The occupant class has been sent to AirbagControlUnit.

### 1.2 Specific Alternative Flow
RFS 4

1. The system sends the error occupant class to AirbagControlUnit.

2. ABORT.

Postcondition: The error occupant class has been sent to AirbagControlUnit.

### 1.3 Bounded Alternative Flow
RFS 1-4

1. IF the voltage is out of range THEN

2. The system sets VoltageError as detected.

3. The system resets and clears classification filter.

4. RESUME STEP 1.

5. ENDIF

Postcondition: The VoltageError has been detected AND The classification filter has been reset.


##Use Case: Self Diagnosis

###BriefDescription
The system performs self diagnosis.

###Precondition
The system has been initialized.

### 2.1 Basic Flow
1. The system sets MeasurementDeviceError as not detected.

2. The system requests TemperatureSensorStatus from the TemperatureSensor.

3. The system VALIDATES THAT the TemperatureSensor is valid.

4. The system requests SeatStatus from the SeatSensor.

5. The system VALIDATES THAT the SeatSensor is valid.

Postcondition: There is no MeasurementDeviceError detected.

### 2.2 Specific Alternative Flow
RFS 3

1. The system sets TemperatureSensorError as detected.

2. RESUME STEP 4.

Postcondition: The TemperatureSensorError has been detected.

### 2.2 Specific Alternative Flow
RFS 5

1. The system sets SeatSensorError as detected.

Postcondition: The SeatSensorError has been detected.


##Use Case: Classify Occupancy Status

###BriefDescription
The system measures the occupancy status via the SeatSensor and derives the occupant class for airbag control.

###Precondition
The system has done the self diagnosis.

### 3.1 Basic Flow
1. The system requests temperature from the TemperatureSensor.

2. The system sets TemperatureError as not detected.

3. The system VALIDATES THAT the temperature is valid.

4. The system VALIDATES THAT the seat is not empty.

5. The system VALIDATES THAT the weight on seat is above 20 kg.

6. The system sets occupant class as adult.

Postcondition: The adult occupant class has been derived.

### 3.2 Specific Alternative Flow
RFS 3

1. The system sets TemperatureError as detected.

4. RESUME STEP 4.

Postcondition: The TemperatureRangeError has been detected.

### 3.3 Specific Alternative Flow
RFS 4

1. The system sets occupant class as empty.

Postcondition: The empty occupant class has been derived.

### 3.4 Specific Alternative Flow
RFS 5

1. The system sets occupant class as child.

Postcondition: The child occupant class has been derived.
