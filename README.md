# meesho-logistics.sql
-- Create the Orders table
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    order_date DATE,
    status VARCHAR(20)
);

-- Create the Delivery_Partners table
CREATE TABLE Delivery_Partners (
    partner_id INT PRIMARY KEY,
    name VARCHAR(100),
    phone VARCHAR(15),
    vehicle_type VARCHAR(20)
);

-- Create the Shipments table
CREATE TABLE Shipments (
    shipment_id INT PRIMARY KEY,
    order_id INT,
    partner_id INT,
    dispatch_date DATE,
    delivery_date DATE,
    status VARCHAR(20),
    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (partner_id) REFERENCES Delivery_Partners(partner_id)
);

-- Create the Returns table
CREATE TABLE Returns (
    return_id INT PRIMARY KEY,
    order_id INT,
    return_reason VARCHAR(255),
    refund_status VARCHAR(20),
    FOREIGN KEY (order_id) REFERENCES Orders(order_id)
);


INSERT INTO Orders (order_id, customer_id, product_id, order_date, status, delivery_partner_id)
VALUES
(1, 101, 301, '2024-01-10', 'Shipped', 1),
(2, 102, 302, '2024-01-12', 'Pending', 2),
(3, 103, 303, '2024-01-15', 'Delivered', 3),
(4, 104, 304, '2024-01-18', 'Shipped', 4);

INSERT INTO Delivery_Partners (partner_id, name, phone, vehicle_type, availability_status)
VALUES
(1, 'Ravi Singh', '8888888888', 'Truck', 'Available'),
(2, 'Anjali Gupta', '7777777777', 'Bike', 'Unavailable'),
(3, 'Rajesh Patel', '6666666666', 'Van', 'Available'),
(4, 'Meera Roy', '5555555555', 'Truck', 'Available');

INSERT INTO Shipments (shipment_id, order_id, partner_id, dispatch_date, delivery_date, status)
VALUES
(1, 1, 1, '2024-01-10', '2024-01-12', 'Delivered'),
(2, 2, 2, '2024-01-12', '2024-01-14', 'Pending'),
(3, 3, 3, '2024-01-15', '2024-01-18', 'Delivered'),
(4, 4, 4, '2024-01-18', '2024-01-20', 'Shipped');

INSERT INTO Returns (return_id, order_id, customer_id, return_reason, refund_status)
VALUES
(1, 1, 101, 'Damaged Product', 'Refunded'),
(2, 3, 103, 'Wrong Product Delivered', 'Pending'),
(3, 4, 104, 'Customer Changed Mind', 'Pending');




