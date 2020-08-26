# Drone-Delivery-Database

Collaborators: Haoran Chen, Sang Hun Jo


A MySQL database interface for a mock application.

### Project Description

  The ongoing pandemic has stimulated the greater increase in customer needs for convenient and fast delivery application.
To satisfy their needs, we have decided to use drone technology instead of automobiles because drones can provide the delivery service wherever customers are and drones can easily fulfill the service in the rush hour. 
  To make the application, we have first made a database that includes relationships and characteristics of Customer, Store Staff, Item, Order, Payment, Payment Method, Drone, Drone Activity History and Drone Agent. To avoid data redundancy, we have normalized agents and store tables to BCNF in the beginning. We have mainly used JDBC to make a model and controller for our database. Model is designed to perform basic CRUD queries to our database, whereas the controller is used to perform more complex queries and fundamental logics behind each query. 
  Finally, we have used Jswing to design our graphical user interface for actual users to use the database system comfortably. Our system is robustly keeping any change on our database. As such, when we re-launch the application, it loads the same data as the latest changes. 


### ER Diagram:

<img src="https://github.com/chen-yifu/Drone-Delivery-Database/blob/master/ER%20Diagram.png"
     alt="ER Diagram"
     style="float: left; margin-right: 10px;" />






### Relational Schema Definition:
Store_Staff(__id__:int, name: string, password: string, phone: int, email: string, address: string, role: string)   Candidate Keys(id)

Customer(__id__:int, name: string, password: string, phone: int, email: string, address: string, VIP_level: string, customer_since: date) Candidate Keys(id)

Drone_Agent(__id__:int, name: string, password: string, phone: int, email: string, address: string, flight_experience: string) Candidate Keys(id)

Drone(__id__:int, model:string, capacity:int, status_id: int, gps_location: string, status: string)

Drone_Activity_History(__id__:int, drone_id:int, order_id:int, status: string, update_at: datetime, create_at: datetime, gps_location: string) FK drone_id REFERENCES Drone; FK order_id REFERENCES Order 

Payment (__payment_id__:int, order_id:int, payment_method_id: int, SN:string, amount: real, status:string) FK order_id REFERENCES Order; FK payment_method_id REFERENCES Method

Payment_Method (__id__:int, name:string, comment:string)

Order(__id__:int, status:string, comment:string, customer_id:int, payment_id:int, drone_history_id: int, delivery_address:string) FK customer_id REFERENCES Customer; FK payment_id REFERENCES Payment; FK drone_history_id REFERENCES Drone_Activity_History

Customer_Makes_Order(__order_id__:int, customer_id:int, order_time:timestamp) FK customer_id REFERENCES Customer; FK order_id REFERENCES order

Staff_Fulfills_Order (__staff_id__:int, __order_id__:int, fulfill_time:timestamp) FK staff_id REFERENCES Staff; FK order_id REFERENCES order

Drone_Delivers_Order (order_id__:int, __drone_id__:int, deliver_status:string, estimated_time:int, delivery_start_time:timestamp, deliver_status:string) FK order_id REFERENCES Order; FK drone_id REFERENCES Drone

Item (__name__:string,__store_id__:int, ingredients:list of string, calorie:int, price:real) FK store_id REFERENCES Store

Order_Contains_Item (__order_id__:int,__item_name__:string,__store_id__:int, quantity:int) FK order_id REFERENCES Order, item_name REFERENCES Item, store_id REFERENCES Store

Store (__id:__int, break_time: timestamp, close_hour: timestamp, open_hour: timestamp, phone: int, address: string, name:string, rating: list of int, type: string)

Store_Staff_Runs_Store(__staff_id__:int, __store_id__:int, since:date) FK staff_id REFERENCES Store_Staff, store_id REFERENCES Store
