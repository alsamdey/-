<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام طلبات المواد الغذائية</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            padding: 15px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 100%;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .header {
            background: linear-gradient(135deg, #e62e04, #ff5e14);
            color: white;
            padding: 20px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 1.5rem;
            margin-bottom: 10px;
        }
        
        .search-box {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 25px;
            margin: 15px 0;
            font-size: 16px;
        }
        
        .categories {
            display: flex;
            overflow-x: auto;
            padding: 10px 0;
            margin-bottom: 10px;
        }
        
        .category-btn {
            padding: 8px 15px;
            background: #f1f1f1;
            border-radius: 20px;
            margin: 0 5px;
            white-space: nowrap;
            border: none;
        }
        
        .category-btn.active {
            background: #e62e04;
            color: white;
        }
        
        .products-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            padding: 10px;
        }
        
        .product-card {
            background: white;
            border-radius: 10px;
            padding: 10px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .product-img {
            width: 100%;
            height: 100px;
            object-fit: contain;
            background: #f8f9fa;
            border-radius: 8px;
        }
        
        .product-name {
            font-weight: bold;
            margin: 5px 0;
            font-size: 14px;
        }
        
        .product-price {
            color: #e62e04;
            font-weight: bold;
        }
        
        .quantity-controls {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-top: 5px;
        }
        
        .quantity-btn {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            border: 1px solid #ddd;
            background: white;
            font-weight: bold;
        }
        
        .quantity-input {
            width: 40px;
            text-align: center;
            margin: 0 5px;
            padding: 5px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        
        .cart-section {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: white;
            border-radius: 15px 15px 0 0;
            padding: 15px;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.1);
        }
        
        .cart-items {
            max-height: 150px;
            overflow-y: auto;
            margin-bottom: 10px;
        }
        
        .cart-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #eee;
        }
        
        .checkout-btn {
            background: linear-gradient(135deg, #e62e04, #ff5e14);
            color: white;
            border: none;
            padding: 15px;
            border-radius: 25px;
            width: 100%;
            font-weight: bold;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>نظام طلبات المواد الغذائية</h1>
            <p>إدارة طلبات الجملة بأحدث التقنيات</p>
        </div>
        
        <input type="text" class="search-box" placeholder="🔍 ابحث عن منتج...">
        
        <div class="categories">
            <button class="category-btn active">الكل</button>
            <button class="category-btn">معلبات</button>
            <button class="category-btn">مشروبات</button>
            <button class="category-btn">حلويات</button>
            <button class="category-btn">تنظيف</button>
            <button class="category-btn">ألبان</button>
        </div>
        
        <div class="products-grid" id="products-container">
            <!-- المنتجات تُضاف هنا -->
        </div>
    </div>
    
    <div class="cart-section">
        <div class="cart-items" id="cart-items">
            <p style="text-align: center; color: #666;">السلة فارغة</p>
        </div>
        <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
            <span>المجموع:</span>
            <span id="cart-total">0.00 ريال</span>
        </div>
        <button class="checkout-btn" onclick="checkout()">تأكيد الطلب</button>
    </div>

    <script>
        // بيانات المنتجات
        const products = [
            { id: 1, name: "أرز بسمتي", category: "معلبات", price: 35, image: "https://via.placeholder.com/150/
