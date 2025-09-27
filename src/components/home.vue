<template>
    <div>
        <div id="app">
            <header>
                <div class="header-content">
                    <div class="logo">
                        <i>🛒</i> 商品货架
                    </div>
                </div>
            </header>
            
            <div class="container">
                <div class="main-content">
                    <div class="sidebar">
                        <h3>商品分类</h3>
                        <ul class="categories">
                            <li v-for="category in categories" 
                                :key="category.id" 
                                :class="{ active: selectedCategory === category.id }"
                                @click="selectCategory(category.id)">
                                {{ category.name }}
                            </li>
                        </ul>
                    </div>
                    
                    <main class="products">
                        <!-- 这里改为使用 filteredProducts 而不是 products -->
                        <div class="product-card" v-for="product in filteredProducts" :key="product.id">
                            <div class="product-image" :style="{ backgroundImage: 'url(' + product.image + ')' }"></div>
                            <div class="product-info">
                                <div class="product-title">{{ product.name }}</div>
                                <div class="product-price">¥{{ product.price }}</div>
                                <div class="product-actions">
                                    <div class="view-details">MoQ≥50pics</div>
                                    <div class="add-to-cart">Contact</div>
                                </div>
                            </div>
                        </div>
                    </main>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                title: 'Hello',
                selectedCategory: 0,
                categories: [
                    { id: 0, name: '全部商品' },
                    { id: 1, name: '电子产品' },
                    { id: 2, name: '家居用品' },
                    { id: 3, name: '服装' },
                    { id: 4, name: '食品饮料' }
                ],
                products: [
                    { id: 1, name: '智能手机', price: 2999, category: 1, image: '/image/tx2.jpg' },
                    { id: 2, name: '笔记本电脑', price: 5999, category: 1, image: '/image/tx2.jpg' },
                    { id: 3, name: '智能手表', price: 1299, category: 1, image: '/image/tx2.jpg' },
                    { id: 4, name: '沙发', price: 2599, category: 2, image: '/image/tx2.jpg' },
                    { id: 5, name: '餐桌', price: 1599, category: 2, image: '/image/tx2.jpg' },
                    { id: 6, name: 'T恤', price: 79, category: 1, image: '/image/tx2.jpg' },
                    { id: 7, name: 'T恤', price: 79, category: 1, image: '/image/tx1.jpg' },
					{ id: 8, name: 'sweat', price: 169, category: 1, image: '/image/sw1.jpg' },
					{ id: 9, name: 'sweat', price: 169, category: 1, image: '/image/sw2.jpg' },
					{ id: 10, name: 'jack', price: 189, category: 1, image: '/image/jack1.jpg' },
					{ id: 11, name: 'jack', price: 189, category: 1, image: '/image/jack2.jpg' },
                    { id: 18, name: '咖啡', price: 39, category: 4, image: '/image/tx2.jpg' },
                    { id: 19, name: '零食礼包', price: 89, category: 4, image: '/image/tx2.jpg' },
                    { id: 110, name: '耳机', price: 399, category: 1, image: '/image/tx2.jpg' }
                ],
            }
        },
        
        onLoad() {
            // 可以在这里添加页面加载时的逻辑
        },
        
        computed: {
            // 修复计算属性的语法
            filteredProducts() {
                                
                // 如果选中的是"全部商品"(id为0)，直接返回所有商品
                if (this.selectedCategory === 0) {
                    return this.products;
                }
                
                // 根据选中的分类进行筛选
                return this.products.filter(product => product.category === this.selectedCategory);
            }
        },
        
        methods: {
            selectCategory(categoryId) {
                
                this.selectedCategory = categoryId;
            },
        }
    }
</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    
    body {
        background-color: #f5f7fa;
        color: #333;
        line-height: 1.6;
    }
    
    .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 20px;
    }
    
    header {
        background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
        color: white;
        padding: 20px 0;
        border-radius: 10px;
        margin-bottom: 30px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    }
    
    .header-content {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0 20px;
    }
    
    .logo {
        font-size: 28px;
        font-weight: 700;
        display: flex;
        align-items: center;
    }
    
    .logo i {
        margin-right: 10px;
        font-size: 32px;
    }
    
    .main-content {
        display: flex;
        gap: 20px;
    }
    
    .sidebar {
        flex: 0 0 250px;
        background: white;
        border-radius: 10px;
        padding: 20px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
    }
    
    .sidebar h3 {
        margin-bottom: 15px;
        padding-bottom: 10px;
        border-bottom: 1px solid #eee;
        color: #6a11cb;
    }
    
    .categories {
        list-style: none;
    }
    
    .categories li {
        padding: 10px 15px;
        margin-bottom: 5px;
        border-radius: 5px;
        cursor: pointer;
        transition: all 0.3s ease;
    }
    
    .categories li:hover, .categories li.active {
        background-color: #6a11cb;
        color: white;
    }
    
    .products {
        flex: 1;
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
        gap: 20px;
    }
    
    .product-card {
        background: white;
        border-radius: 10px;
        overflow: hidden;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
        transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    
    .product-card:hover {
        transform: translateY(-5px);
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
    }
    
    .product-image {
        height: 403px;
        background-size: cover;
        background-position: center;
    }
    
    .product-info {
        padding: 10px;
    }
    
    .product-title {
		font-weight: 600;
        /* font-size: 14px;
        
        margin-bottom: 10px;
        height: 50px; */
        overflow: hidden;
    }
    
    .product-price {
        color: #6a11cb;
        font-size: 20px;
        font-weight: 700;
        /* margin-bottom: 15px; */
    }
    
    .product-actions {
        display: flex;
        justify-content: space-between;
    }
    
    .add-to-cart {
        background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
        color: white;
        border: none;
        padding: 8px 15px;
        border-radius: 5px;
        cursor: pointer;
        font-weight: 600;
        transition: all 0.3s ease;
    }
    
    .add-to-cart:hover {
        opacity: 0.9;
        transform: scale(1.05);
    }
    
    .view-details {
        background: #f1f2f6;
        color: #333;
        border: none;
        padding: 8px 15px;
        border-radius: 5px;
        cursor: pointer;
        font-weight: 600;
        transition: all 0.3s ease;
    }
    
    .view-details:hover {
        background: #dfe4ea;
    }
    
    @media (max-width: 768px) {
        .main-content {
            flex-direction: column;
        }
        
        .sidebar {
            flex: none;
        }
    }
</style>