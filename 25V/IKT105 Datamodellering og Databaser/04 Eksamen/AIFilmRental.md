**Potential entitites**:
branch: branch address( street, city, state, zip code), telephone numbers, branch number (unique), branch name
staff: name, position, salary, staff number (unique)
	manager 
	supervisor
	staff
videos: catalog nu mber (identifies content), video number (unique per), title, category, daily rental rate, purchase price, status (available or not), main actor names and characters, director
	category: Action, adult children thriller horror, sci-fi
	Likely that status is a generated value based on if it is currently being rented.
customer: first name, last name, address, date registered, member number (unique), staff responsible (name)

VideoRental( Video rented): rental number (unique), member full name, member number, video number, title, daily rental cost, date rented out, date returned

Video supplier: supplier number, name, address, telephone number, status.
Video order: order number, supplier number, supplier address, video catalog number, video title, video purchase price, quantity, date order placed, date order received, address of brach.
	Why not branch number?





**Constraints:**
`Branch` has max 3 telephone numbers
`Branch` has 1 `manager`, and 1 or more `supervisors` and a number of `staff`.
(`Supervisor`  supervises a group of `staff`.) Not specified to keep track of.
Several copy of each `video` at `branch`.
`Staff` registers `Customer/member` (says name is noted, but might link staff.)
`Customer/Member` rents up to 10 `videos` at one time. (handle at higher level, perhaps in program)
`Customer/member` can register at more than one `branch` (same member number)
**Relationships**
 One `Branch` has many `Staff` members.
 One `Branch` has many `Videos` (copies). This will likely be a many-to-many relationship resolved with a linking table holding the `video number` and `status`.
 One `Member` can rent many `Videos`, and one `Video` can be rented by many `Members` over time (many-to-many, resolved by the `Rentals` entity).
One `Branch` has many `Members`.
One `Video` can have many `Actors` and one `Actor` can be in many `Videos` (many-to-many, requiring a linking table). Similarly for `Directors`.
One `VideoSupplier` can have many `VideoOrders`.
One `Branch` can receive many `VideoOrders`.

**Things to keep in mind**
Videos should be updated when an order is delivered. 
Telephone numbers for `branch` and main actors for `video` are multi-valued.
`status` of supplier, what is that?
Information in video order regarding video information  needs to be kept since it should be "saved" in a video upon delivery.

Branch HAS 1 Superviosr. how to enforce.

Purchase price is per video since same catalog can be bought from different suppliers
![[25V/IKT105 Datamodellering og Databaser/img/image-4.png]]
Check if staff number can be used or only staff name



FIX CONSTRAINTS