# Yoraa Clothing Shop - Backend API Documentation

## Base URL
```
http://localhost:8080
```

## Authentication
All protected endpoints require a Bearer token in the Authorization header:
```
Authorization: Bearer <your_jwt_token>
```

## Response Format
All API responses follow a standard format:
```json
{
  "data": {},
  "message": "Success message",
  "success": true,
  "statusCode": 200,
  "error": null
}
```

---

## 🔐 Authentication Endpoints

### POST `/api/auth/login`
Login with email and password.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

### POST `/api/auth/signup`
Register a new user account.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "password123",
  "name": "John Doe",
  "phone": "+1234567890"
}
```

### POST `/api/auth/login/firebase`
Login using Firebase authentication.

### POST `/api/auth/signup/firebase`
Signup using Firebase authentication.

### POST `/api/auth/generate-otp`
Generate OTP for phone verification.

**Request Body:**
```json
{
  "phone": "+1234567890"
}
```

### POST `/api/auth/verifyFirebaseOtp`
Verify OTP sent via Firebase.

**Request Body:**
```json
{
  "phone": "+1234567890",
  "otp": "123456"
}
```

### POST `/api/auth/sendVerificationEmail`
Send email verification link.

### POST `/api/auth/verifyEmail`
Verify email address.

### POST `/api/auth/resetPassword`
Reset user password.

### GET `/api/auth/logout`
Logout user (clear session/tokens).

### DELETE `/api/auth/deleteUser` 🔒
Delete user account (requires authentication).

### GET `/api/auth/totalUsersCount` 🔒
Get total number of registered users (admin only).

---

## 👤 User Management

### GET `/api/user/getUser` 🔒
Get current user information.

### PATCH `/api/user/:id`
Update user information by ID.

**Request Body:**
```json
{
  "name": "Updated Name",
  "email": "updated@example.com"
}
```

### GET `/api/user/getAlluser` 🔒
Get all users (admin only).

---

## 👤 User Profile

### GET `/api/userProfile/getProfile` 🔒
Get user profile information.

### POST `/api/userProfile/postProfile` 🔒
Create user profile with image upload.

**Form Data:**
- `image`: Profile image file
- `bio`: User bio
- `dateOfBirth`: Date of birth
- Other profile fields

### PUT `/api/userProfile/updateProfile` 🔒
Update user profile with image upload.

### GET `/api/userProfile/getProfileByUserId/:userId` 🔒
Get user profile by user ID.

---

## 🏷️ Categories

### POST `/api/categories` 🔒👑
Create a new category (admin only).

**Form Data:**
- `name`: Category name
- `description`: Category description
- `image`: Category image file

### GET `/api/categories`
Get all categories.

### GET `/api/categories/:id`
Get category by ID.

### PUT `/api/categories/:id` 🔒👑
Update category by ID (admin only).

### DELETE `/api/categories/:id` 🔒👑
Delete category by ID (admin only).

### GET `/api/categories/totalCategories` 🔒
Get total number of categories.

---

## 🏷️ Subcategories

### POST `/api/subcategories` 🔒👑
Create a new subcategory (admin only).

**Form Data:**
- `name`: Subcategory name
- `categoryId`: Parent category ID
- `description`: Subcategory description
- `image`: Subcategory image file

### GET `/api/subcategories`
Get all subcategories.

### GET `/api/subcategories/category/:categoryId`
Get subcategories by category ID.

### GET `/api/subcategories/:id`
Get subcategory by ID.

### PUT `/api/subcategories/:id` 🔒👑
Update subcategory by ID (admin only).

### DELETE `/api/subcategories/:id` 🔒👑
Delete subcategory by ID (admin only).

### GET `/api/subcategories/totalSubcategories` 🔒
Get total number of subcategories.

---

## 🛍️ Items/Products

### POST `/api/items` 🔒👑
Create a new item (admin only).

**Form Data:**
- `name`: Item name
- `description`: Item description
- `price`: Item price
- `categoryId`: Category ID
- `subCategoryId`: Subcategory ID
- `image`: Item image file
- `stock`: Stock quantity
- `brand`: Brand name
- `size`: Available sizes
- `color`: Available colors

### GET `/api/items`
Get all items with pagination and filtering.

**Query Parameters:**
- `page`: Page number (default: 1)
- `limit`: Items per page (default: 10)
- `category`: Category ID filter
- `subcategory`: Subcategory ID filter
- `minPrice`: Minimum price filter
- `maxPrice`: Maximum price filter
- `search`: Search term

### POST `/api/items/filter`
Get items by advanced filters.

**Request Body:**
```json
{
  "categories": ["categoryId1", "categoryId2"],
  "priceRange": {
    "min": 100,
    "max": 1000
  },
  "sizes": ["S", "M", "L"],
  "colors": ["red", "blue"],
  "brands": ["Brand1", "Brand2"]
}
```

### GET `/api/items/:id`
Get item by ID.

### GET `/api/items/category/:categoryId`
Get items by category ID.

### GET `/api/items/subcategory/:subCategoryId`
Get items by subcategory ID.

### PUT `/api/items/:id` 🔒👑
Update item by ID (admin only).

### DELETE `/api/items/:id` 🔒👑
Delete item by ID (admin only).

### GET `/api/items/download` 🔒👑
Download all items as JSON (admin only).

---

## 📄 Item Details

### POST `/api/itemDetails/:itemId` 📤
Create item details for a specific item with multiple file uploads.

**Form Data:**
- `images`: Up to 25 image files
- `videos`: Up to 25 video files  
- `sizeChartInch`: Size chart in inches (1 file)
- `sizeChartCm`: Size chart in centimeters (1 file)
- `sizeMeasurement`: Size measurement file (1 file)
- Other item detail fields

### GET `/api/itemDetails`
Get all item details.

### GET `/api/itemDetails/:itemId`
Get detailed information for a specific item.

### PUT `/api/itemDetails/update/:itemId` �
Update item details for a specific item with file uploads.

### DELETE `/api/itemDetails/:id`
Delete item details by ID.

### POST `/api/itemDetails/delete-media/:itemId`
Delete specific media from item details.

**Request Body:**
```json
{
  "mediaType": "images",
  "mediaUrls": ["url1", "url2"]
}
```

### GET `/api/itemDetails/zero-stock`
Get item details for items with zero stock.

### GET `/api/itemDetails/out-of-stock/count`
Get count of out-of-stock items.

### GET `/api/itemDetails/download` 🔒👑
Download all item details as JSON (admin only).

---

## ❤️ Wishlist

### POST `/api/wishlist/add` 🔒
Add item to wishlist.

**Request Body:**
```json
{
  "itemId": "item_id_here"
}
```

### GET `/api/wishlist` 🔒
Get user's wishlist items.

### DELETE `/api/wishlist/remove/:itemId` 🔒
Remove item from wishlist.

### DELETE `/api/wishlist/clear` 🔒
Clear entire wishlist.

---

## 🛒 Shopping Cart

### POST `/api/cart` 🔒
Add item to cart.

**Request Body:**
```json
{
  "itemId": "item_id_here",
  "quantity": 2,
  "size": "M",
  "color": "blue"
}
```

### GET `/api/cart/user` 🔒
Get user's cart items.

### PATCH `/api/cart/:id` 🔒
Update cart item (quantity, size, color).

**Request Body:**
```json
{
  "quantity": 3,
  "size": "L"
}
```

### DELETE `/api/cart/:id` 🔒
Remove specific cart item.

### DELETE `/api/cart/user/delete` 🔒
Clear entire cart.

### DELETE `/api/cart/item/:itemId` 🔒
Remove cart item by item ID.

---

## 📍 Address Management

### POST `/api/address/createAddress` 🔒
Add new address.

**Request Body:**
```json
{
  "street": "123 Main St",
  "city": "Mumbai", 
  "state": "Maharashtra",
  "pincode": "400001",
  "country": "India",
  "phone": "+91-9876543210",
  "isDefault": true
}
```

### GET `/api/address/user` 🔒
Get user's addresses.

### PATCH `/api/address/updateById/:id` 🔒
Update address by ID.

### DELETE `/api/address/deleteById/:id` 🔒
Delete address by ID.

---

## 📦 Orders

### GET `/api/orders/getAllByUser` 🔒
Get all orders for the authenticated user.

### POST `/api/orders/cancel/:order_id`
Cancel a specific order by order ID.

**Request Body:**
```json
{
  "reason": "Customer request"
}
```

### GET `/api/orders/getAllOrder` 🔒
Get all orders sorted (admin only).

### GET `/api/orders/delivered` 🔒
Get delivered orders for the authenticated user.

### GET `/api/orders/exchange-orders` 🔒
Get exchange orders for the authenticated user.

### GET `/api/orders/return-orders` 🔒
Get return orders for the authenticated user.

### GET `/api/orders/status-counts` 🔒
Get counts of orders by status for the authenticated user.

### POST `/api/orders/exchange` 🔒📤
Create an exchange order with optional image uploads.

**Form Data:**
- `orderId`: Original order ID
- `itemId`: Item ID to exchange
- `reason`: Reason for exchange
- `images`: Up to 3 image files (optional)

### POST `/api/orders/return` 🔒�
Create a return order with optional image uploads.

**Form Data:**
- `orderId`: Original order ID
- `itemId`: Item ID to return
- `reason`: Reason for return
- `images`: Up to 3 image files (optional)

### POST `/api/orders/shiprocket/auth`
Authenticate with Shiprocket API.

### GET `/api/orders/shiprocket/track/:awbCode`
Get Shiprocket tracking information by AWB code.

---

## 💳 Payment (Razorpay)

### POST `/api/razorpay/create-order` 🔒
Create Razorpay order.

**Request Body:**
```json
{
  "amount": 1998,
  "currency": "INR"
}
```

### POST `/api/razorpay/verify-payment`
Verify Razorpay payment.

**Request Body:**
```json
{
  "razorpay_order_id": "order_id",
  "razorpay_payment_id": "payment_id",
  "razorpay_signature": "signature"
}
```

---

## ⭐ Reviews

### POST `/api/reviews/user/:itemId/reviews` 🔒
Create review for an item.

**Request Body:**
```json
{
  "rating": 5,
  "comment": "Great product!",
  "title": "Excellent quality"
}
```

### GET `/api/reviews/user/:itemId/reviews`
Get reviews for an item.

### PUT `/api/reviews/user/:itemId/reviews/:reviewId` 🔒
Update review.

### DELETE `/api/reviews/user/:itemId/reviews/:reviewId` 🔒
Delete review.

### GET `/api/reviews/user/:itemId/average-rating`
Get average rating for an item.

### GET `/api/reviews/public/:itemId/reviews`
Get public reviews for an item.

### GET `/api/reviews/public/:itemId/average-rating`
Get public average rating for an item.

### POST `/api/reviews/admin/:itemDetailsId/reviews` 🔒👑
Create fake review (admin only).

### PUT `/api/reviews/admin/:itemDetailsId/review-settings` 🔒👑
Update review settings (admin only).

---

## 🎟️ Promo Codes

### POST `/api/promoCode/promo-codes/validate`
Validate promo code.

**Request Body:**
```json
{
  "code": "SAVE20",
  "orderAmount": 1000
}
```

### POST `/api/promoCode/admin/promo-codes` 🔒👑
Create promo code (admin only).

**Request Body:**
```json
{
  "code": "SAVE20",
  "discountType": "percentage",
  "discountValue": 20,
  "minOrderAmount": 500,
  "maxDiscountAmount": 200,
  "validFrom": "2024-01-01",
  "validUntil": "2024-12-31",
  "usageLimit": 100,
  "isActive": true
}
```

### GET `/api/promoCode/admin/promo-codes` 🔒👑
Get all promo codes (admin only).

### PUT `/api/promoCode/admin/promo-codes/:id` 🔒👑
Update promo code (admin only).

### DELETE `/api/promoCode/admin/promo-codes/:id` 🔒👑
Delete promo code (admin only).

---

## 🔍 Filters

### POST `/api/filters`
Create a new filter.

**Request Body:**
```json
{
  "name": "Size",
  "type": "size",
  "options": ["S", "M", "L", "XL"],
  "category": "clothing"
}
```

### GET `/api/filters`
Get all available filters.

### GET `/api/filters/:id`
Get filter by ID.

### PUT `/api/filters/:id`
Update filter by ID.

### DELETE `/api/filters/:id`
Delete filter by ID.

---

## 📤 Bulk Upload

### POST `/api/bulkUpload/items` 🔒👑
Bulk upload items via Excel/CSV (admin only).

**Form Data:**
- `file`: Excel/CSV file with item data

### POST `/api/bulkUpload/categories` 🔒👑
Bulk upload categories via Excel/CSV (admin only).

---

## 📱 Notifications

### POST `/api/send-notification` 🔒👑
Send push notification (admin only).

**Request Body:**
```json
{
  "title": "New Offer!",
  "body": "50% off on selected items",
  "userId": "user_id", // optional, for targeted notification
  "data": {
    "type": "offer",
    "itemId": "item_id"
  }
}
```

### GET `/api/notifications` 🔒
Get user notifications.

---

## 📋 Privacy Policy

### GET `/api/privacyPolicy/get` 🔒
Get privacy policy content.

### POST `/api/privacyPolicy/post`
Create privacy policy section.

**Request Body:**
```json
{
  "title": "Data Collection",
  "content": "We collect the following information..."
}
```

### GET `/api/privacyPolicy/get/:title` 🔒
Get privacy policy section by title (commented out in code).

---

## ⚠️ Issues Found & Fixes Needed

### 1. MongoDB Connection Error
**Issue:** `MongooseServerSelectionError: connect ECONNREFUSED ::1:27017`

**Fix:** Make sure MongoDB is running locally:
```bash
# Windows (if MongoDB is installed locally)
net start MongoDB

# Or start MongoDB service manually
mongod --dbpath "C:\data\db"

# Alternative: Use MongoDB Atlas (cloud)
# Update MONGO_URI in .env to MongoDB Atlas connection string
```

### 2. Privacy Policy Route Error
**Issue:** Invalid route path in `index.js` line 53:
```javascript
app.use("/api privacyPolicy", privacyPolicyRoutes); // Missing slash
```

**Fix:** Should be:
```javascript
app.use("/api/privacyPolicy", privacyPolicyRoutes);
```

### 3. Missing Product Routes
**Issue:** `Product.js` routes are commented out but not being used.

**Fix:** Either implement or remove the commented Product routes file.

---

## Status Codes

- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden (Admin access required)
- `404` - Not Found
- `500` - Internal Server Error

## Symbols

- 🔒 - Authentication required
- 👑 - Admin role required
- 📤 - File upload supported

## Environment Variables Required

```env
MONGO_URI=mongodb://localhost:27017/yoraa1
SECRET_KEY=your_jwt_secret
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_REGION=ap-south-1
AWS_BUCKET_NAME=your_s3_bucket
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
FIREBASE_PROJECT_ID=your_firebase_project_id
FIREBASE_PRIVATE_KEY=your_firebase_private_key
FIREBASE_CLIENT_EMAIL=your_firebase_client_email
```

## Notes

1. All authenticated endpoints require a valid JWT token.
2. Admin endpoints require both authentication and admin role.
3. File uploads are handled via multipart/form-data.
4. Images are uploaded to AWS S3.
5. Payments are processed through Razorpay.
6. Push notifications use Firebase Cloud Messaging.
7. Database is MongoDB with Mongoose ODM.

---

*Last updated: August 3, 2025*
