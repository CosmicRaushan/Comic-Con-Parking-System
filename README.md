# Comic-Con-Parking-System

Code of Comic-Con Parking System

Vehicle [icon: car] {
  vehicle_id INT [pk]
  name string NOT NULL
  vichels_category varchar(20) NOT NULL ['bikes', 'cars', 'suv', 'cabs', 'EV']
  vechil_number varchar(30) NOT NULL
}

Parked_area [icon: aws-local-zones]{
  parking_id INT [pk]
  parking_spot string NOT NULL ['VIP', 'exhibitors', 'staff', 'EV charging']
  parking_zone string NOT NULL ['zoneA', zoneB']
}

Session [icon: clock]{
  session_id INT [pk]
  parking_id INT [fk]
  vehicle_id INT [fk]
  enterAt timestamp NOT NULL
  existAt timestamp NOT NULL
  date DATE  NOT NULL
}

Reservations [icon: aws-reserved-instance-reporting]{
  reservation_id INT [pk]
  vehicle_id INT [fk]
  parking_id INT [fk]
  start_at timestamp
  end_at timestamp
  status string ['active', cancelled', 'complete'] NOT NULL
  reservation_fee INT
  payment_status string ['paid', 'pending'] NOT NULL
}


Tickets [icon: ticket]{
  ticket_id INT [pk]
  session_id INT [fk]
  fee INT NOT NULL
}

Payments [icon: dollar-sign]{
  payment_id INT [pk]
  ticket_id INT optional NOT NULL[fk]
  reservation_id int optional NOT NULL[fk]
  payment_mode string ['online', 'card', 'cash']
  payment_status string ['paid', 'pending', 'failed']
  amount INT
  payment_time timestamp
}


// Relation between tables 


Vehicle.vehicle_id < Session.vehicle_id // one vehicle has multiple session 


Session.session_id - Tickets.session_id // one session has one ticket

Tickets.ticket_id < Payments.ticket_id // ticket 1 -> many payments

Vehicle.vehicle_id < Reservations.vehicle_id // vehicle 1 -> many reservation

Reservations.reservation_id < Payments.reservation_id // reservation 1 -> many payment

Parked_area.parking_id < Reservations.parking_id

Parked_area.parking_id < Session.parking_id
