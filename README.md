CREATE TABLE stations (
    station_id INT AUTO_INCREMENT PRIMARY KEY,
    station_name VARCHAR(255),
    location VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE TABLE trains (
    train_id INT AUTO_INCREMENT PRIMARY KEY,
    train_number VARCHAR(50) UNIQUE,
    train_type VARCHAR(100),  -- , express, local,.
    capacity INT,  -- Number of seats in the train
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE TABLE routes (
    route_id INT AUTO_INCREMENT PRIMARY KEY,
    train_id INT,  -- Foreign key to the trains table
    station_id INT,  -- Foreign key to the stations table
      departure_time DATETIME,
    arrival_time DATETIME,
    FOREIGN KEY (train_id) REFERENCES trains(train_id),
    FOREIGN KEY (station_id) REFERENCES stations(station),
     created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE passengers (
    passenger_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    phone VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE bookings (
    booking_id INT AUTO_INCREMENT PRIMARY KEY,
    passenger_id INT,  -- Foreign key to passengers
    route_id INT,  -- Foreign key to routes
    seat_number VARCHAR(20),
    booking_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status ENUM('booked', 'cancelled', 'completed') DEFAULT 'booked',
    FOREIGN KEY (passenger_id) REFERENCES passengers(passenger_id),
    FOREIGN KEY (route_id) REFERENCES routes(route_id)
);

INSERT INTO stations (station_name, location)
VALUES
('Kisauni, 'mombasa'),
('Mariakani', 'mtito'),
('Garauge', 'nairobi');


NSERT INTO trains (train_number, train_type, capacity)
VALUES
('TRAIN001', 'Express', 200),
('TRAIN002', 'Local', 100);

INSERT INTO routes (train_id, start_station_id, end_station_id, departure_time, arrival_time)
VALUES
(1, 1, 2, '2025-01-10 08:00:00', '2025-01-10 10:00:00'),


INSERT INTO passengers (first_name, last_name, email, phone)
VALUES
('inocent', 'kiema', '0789231467'),
('Jane', 'akoth', '0987654321');


INSERT INTO bookings (passenger_id, route_id, seat_number)
VALUES
(1, 1, 'A1'),
(2, 2, 'B2');

SELECT r.route_id, t.train_number, s1.station_name AS start_station, s2.station_name AS end_station, r.departure_time, r.arrival_time
FROM routes r
JOIN stations s1 ON r.start_station_id = s1.station_id
JOIN stations s2 ON r.end_station_id = s2.station_id
JOIN trains t ON r.train_id = t.train_id
WHERE s1.station_name = 'kisauni' AND r.departure_time > NOW();
(2, 2, 3, '2025-01-10 09:00:00', '2025-01-10 11:00:00');

