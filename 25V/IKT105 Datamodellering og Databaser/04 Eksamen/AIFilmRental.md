Nouns:
Videos
members
branch
rent
branch: branch address( street, city, state, zip code), telephone numbers (3 lines), branch number (unique)
staff: name, position, salary, staff number (unique)
	manager 
	supervisor (1 or more)
	staff
videos: catalog number (identifies content), video number (unique per), title, category, daily rental rate, purchase price, status (available or not), main actor names and characters, director
	category: Action, adult children thriller horror, sci-fi
	Likely that status is a generated value based on if it is currently being rented.
customer: first name, last name, address, date registered, member number (unique), staff responsible (name)

Rental( Video rented): rental number (unique), member full name, member number, video number, title, daily rental cost, date rented out, date returned

Video supplier: supplier number, name, address, telephone number, status.
video order: order number, supplier number, supplier address, video catalog number, video title, video purchase price






relations:


