# Booking Management System

This project is a Django-based booking platform inspired by services like Airbnb, Booking.com, and Agoda. It allows users to create accounts, list and manage properties, book listings and rooms, process payments, and leave reviews.

## Features

### User Management

- **Registration** (`register_user`):  
  Allows users to create an account with custom user details. Upon successful registration, the user is automatically logged in and redirected to the home page.


- **Login** (`login_user`):  
  Authenticates users using their email and password. Upon successful login, users are redirected to the home page.


- **Logout** (`logout_user`):  
  Logs the user out and redirects them to the home page.

- **Change Password** (`change_password`):  
  Allows users to change their password using Django’s `PasswordChangeForm`. Updates the session upon a successful password change.


- **Update User Profile** (`update_user`):  
  Users can update their account information via the `CustomUserChangeForm` and `ProfileForm`.

- **Delete User Account** (`delete_user`):  
  Authenticated users can delete their account, which removes their profile and redirects them to the home page.


- **User Profile** (`profile`):  
  Displays the profile of the authenticated user.


- **User Detail** (`user_detail`):  
  Shows details of a specific user based on their user ID.


### Listing and Room Management

- **Create Listing** (`create_listing`):  
  Allows hosts to submit a listing with images via `ListingCreationForm` and `ListingImageFormSet`. Upon success, the listing is saved along with its images.


- **Listing List** (`listing_list`):  
  Displays all available listings in the system.


- **Listing Detail** (`listing_detail`):  
  Shows detailed information about a specific listing.


- **Update Listing** (`update_listing`):  
  Allows hosts to update their existing listing and its images.


- **Delete Listing** (`delete_listing`):  
  Allows hosts to delete their listing and its associated images.

- **Create Room** (`create_room`):  
  Allows users to create rooms within a listing using `RoomCreationForm` and `RoomImageFormSet`.


- **Room List** (`room_list`):  
  Displays all available rooms.


- **Room Detail** (`room_detail`):  
  Shows detailed information about a specific room.


- **Update Room** (`update_room`):  
  Allows hosts to update room details and images.
 

- **Delete Room** (`delete_room`):  
  Allows hosts to delete a room and its associated images.

### Booking Management

- **Create Booking** (`booking_create`):  
  Allows users to book a listing or room. The total price is calculated based on the booking dates and room/listing price.


- **Booking List** (`booking_list`):  
  Displays all bookings made by the authenticated user.


- **Booking Detail** (`booking_detail`):  
  Displays detailed information about a specific booking.


### Payment Processing

- **Create Payment** (`payment_create`):  
  Initiates PayPal payment using `PayPalPaymentsForm` and redirects users to PayPal for transaction completion.


- **Payment Success** (`payment_success`):  
  Marks a booking as "Confirmed" and payment as "Paid" after a successful PayPal payment.


- **Payment Cancel** (`payment_cancel`):  
  Handles canceled payments and maintains the booking status.


### Reviews

- **Create Review** (`review_create`):  
  Allows users to leave reviews for a listing after a booking experience.


- **Review List** (`review_list`):  
  Displays a list of reviews for a particular listing.


- **Update Review** (`review_update`):  
  Allows users to update their review for a booking.

- **Delete Review** (`review_delete`):  
  Allows users to delete their own review.

## API Endpoints

### 1. User Management Endpoints

- **POST** `/users/register/`:  
  Register a new user.
  - Request Body:
    - `email` (string): User’s email.
    - `password` (string): User’s password.
    - `profile_picture` (optional, file): User's profile picture.
  - Response: JSON object with user information and registration success message.

- **POST** `/users/update/`:  
  Update the user’s profile.
  - Request Body:
    - `email` (optional, string): New email address.
    - `password` (optional, string): New password.
    - `profile_picture` (optional, file): New profile picture.
  - Response: Success message and updated user information.

- **DELETE** `/users/delete/`:  
  Delete a user account.
  - Response: Success message confirming account deletion.

- **GET** `/users/profile/`:  
  Retrieve the profile of the logged-in user.
  - Response: JSON object containing user profile data.

- **GET** `/users/<int:user_id>/`:  
  Get details of a specific user by their ID.
  - Response: JSON object with user details.

- **POST** `/users/login/`:  
  Log in a user.
  - Request Body:
    - `email` (string): User’s email.
    - `password` (string): User’s password.
  - Response: JSON object containing a token and user information upon successful authentication.

- **POST** `/users/logout/`:  
  Log out the current user.
  - Response: Success message indicating logout.

- **POST** `/users/password/`:  
  Change the current user’s password.
  - Request Body:
    - `old_password` (string): Current password.
    - `new_password` (string): New password.
  - Response: Success message indicating password change.

### 2. Listing Management Endpoints

- **POST** `/listings/create/`:  
  Create a new listing.
  - Request Body:
    - `title` (string): Title of the listing.
    - `description` (string): Description of the listing.
    - `price` (float): Price per night.
    - `images` (optional, list of files): Images for the listing.
  - Response: Success message and listing details.

- **GET** `/listings/`:  
  Retrieve a list of all listings.
  - Response: JSON array containing all listings.

- **GET** `/listings/<int:id>/`:  
  Get the details of a specific listing by its ID.
  - Response: JSON object containing the listing details.

- **PUT** `/listings/<int:id>/update/`:  
  Update a listing’s details.
  - Request Body:
    - `title` (optional, string): New title for the listing.
    - `description` (optional, string): New description for the listing.
    - `price` (optional, float): New price per night.
    - `images` (optional, list of files): New images for the listing.
  - Response: Success message indicating listing update.

- **DELETE** `/listings/<int:id>/delete/`:  
  Delete a listing.
  - Response: Success message confirming listing deletion.

### 3. Room Management Endpoints

- **POST** `/listings/create_room/`:  
  Create a new room within a listing.
  - Request Body:
    - `listing_id` (integer): ID of the listing the room belongs to.
    - `name` (string): Name of the room.
    - `price` (float): Price per night.
    - `images` (optional, list of files): Images for the room.
  - Response: Success message and room details.

- **GET** `/listings/rooms/`:  
  Retrieve all rooms within listings.
  - Response: JSON array of all rooms.

- **GET** `/listings/rooms/<int:id>/`:  
  Retrieve details of a specific room by its ID.
  - Response: JSON object containing room details.

- **PUT** `/listings/rooms/<int:id>/update/`:  
  Update room details.
  - Request Body:
    - `name` (optional, string): New room name.
    - `price` (optional, float): New price per night.
    - `images` (optional, list of files): New images for the room.
  - Response: Success message indicating room update.

- **DELETE** `/listings/rooms/<int:id>/delete/`:  
  Delete a room.
  - Response: Success message confirming room deletion.

### 4. Booking Management Endpoints

- **POST** `/bookings/create/<int:listing_id>/<int:room_id>/`:  
  Create a booking for a specific listing and room.
  - Request Body:
    - `start_date` (string, YYYY-MM-DD): Check-in date.
    - `end_date` (string, YYYY-MM-DD): Check-out date.
    - `number_of_guests` (integer): Number of guests.
  - Response: Success message and booking details.

- **GET** `/bookings/<int:booking_id>/`:  
  Retrieve the details of a specific booking.
  - Response: JSON object containing booking details.

- **GET** `/bookings/list/`:  
  Retrieve a list of all bookings for the logged-in user.
  - Response: JSON array of bookings.

### 5. Payment Management Endpoints

- **POST** `/bookings/payments/<int:booking_id>/create/`:  
  Create a payment for a booking via PayPal.
  - Response: PayPal payment URL and status.

- **GET** `/bookings/payments/<int:booking_id>/<int:payment_id>/success/`:  
  Confirm payment success for a booking.
  - Response: Success message and booking confirmation.

- **GET** `/bookings/payments/<int:booking_id>/cancel/`:  
  Handle payment cancellation.
  - Response: Message indicating payment was canceled.

### 6. General Site Endpoints

- **GET** `/`:  
  Access the homepage.

- **GET** `/about/`:  
  Access the "About" page.

## Technologies Used

- **Backend**: Django
- **Frontend**: HTML, CSS
- **Payment Integration**: PayPal
