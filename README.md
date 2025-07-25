# 📦 Logistics Performance Analytics Hub

> **Expert-Level Power BI Dashboard** for E-commerce Delivery Operations Intelligence

## 🎯 **Project Overview**

This Power BI project demonstrates **enterprise-level data modeling** and **advanced analytics** for logistics and delivery operations. Built using **Star Schema architecture** with **20+ expert DAX measures** and **professional dashboard design**.

### **Key Features:**
- 🏗️ **Star Schema Data Model** with optimized relationships
- 📊 **Advanced DAX Measures** for business intelligence  
- 🎨 **Executive-Level Dashboard** design
- ⚡ **Performance Optimized** data structure
- 📈 **Multi-dimensional Analysis** capabilities

---

## 📊 **Dataset Information**

**Source:** E-commerce Delivery Dataset (Train.csv)
- **Records:** 10,999 shipments
- **Columns:** 12 attributes
- **Domain:** Logistics & Supply Chain Analytics

### **Original Data Structure:**
```
├── ID (Shipment identifier)
├── Warehouse_block (A, B, C, D, F)
├── Mode_of_Shipment (Flight, Road, Ship)
├── Customer_care_calls (2-7 calls)
├── Customer_rating (1-5 stars)
├── Cost_of_the_Product ($96-$310)
├── Prior_purchases (2-10 previous orders)
├── Product_importance (low, medium, high)
├── Gender (M, F)
├── Discount_offered (1-65%)
├── Weight_in_gms (1001-7846 grams)
└── Reached.on.Time_Y.N (0=Late, 1=On Time)
```

---

## 🏗️ **Data Architecture**

### **Star Schema Implementation**

#### **📊 Fact Table: FactShipments_Final**
- **Primary Key:** ShipmentID
- **Metrics:** Cost, Weight, Discount, Prior_purchases, OnTimeDelivery
- **Foreign Keys:** WarehouseKey, ShipmentKey, ProductKey, CustomerKey
- **Rows:** 10,999

#### **🔗 Dimension Tables:**

**DimWarehouse (5 rows):**
```sql
WarehouseKey | WarehouseName
1           | D
2           | F  
3           | A
4           | B
5           | C
```

**DimShipment (3 rows):**
```sql
ShipmentKey | ShipmentMode
1          | Flight
2          | Road
3          | Ship
```

**DimProduct (3 rows):**
```sql
ProductKey | ImportanceLevel
1         | high
2         | low
3         | medium
```

**DimCustomer (30+ rows):**
```sql
CustomerKey | Gender | Customer_rating | Customer_care_calls
1          | F      | 2               | 4
2          | M      | 2               | 2
...        | ...    | ...             | ...
```

---

## 🎯 **DAX Measures Library**

### **📈 Core Performance KPIs**
```dax
On Time Delivery Rate = 
DIVIDE(
    CALCULATE(COUNT(FactShipments_Final[OnTimeDelivery]), FactShipments_Final[OnTimeDelivery] = 1),
    COUNT(FactShipments_Final[OnTimeDelivery]),
    0
) * 100

Total Shipments = COUNT(FactShipments_Final[ShipmentID])

Net Revenue = [Total Revenue] - [Total Discount]
```

### **👥 Customer Analytics**
```dax
Customer Satisfaction Score = 
AVERAGEX(FactShipments_Final, RELATED(DimCustomer[Customer_rating]))

Customer Segment = 
VAR Rating = AVERAGEX(FactShipments_Final, RELATED(DimCustomer[Customer_rating]))
VAR Purchases = AVERAGE(FactShipments_Final[Prior_purchases])
RETURN 
SWITCH(TRUE(),
    Rating >= 4 && Purchases >= 7, "💎 VIP Champions",
    Rating >= 4, "⭐ Loyal Customers", 
    "📊 Regular"
)
```

### **📊 Business Intelligence**
```dax
Weighted Performance Score = 
VAR DeliveryScore = [On Time Delivery Rate] / 100
VAR CostScore = 1 - ([Average Discount Rate] / 100)
RETURN (DeliveryScore * 0.6 + CostScore * 0.4) * 100

Delivery Risk Score = 
VAR CareCalls = AVERAGEX(FactShipments_Final, RELATED(DimCustomer[Customer_care_calls]))
VAR Weight = AVERAGE(FactShipments_Final[Weight_in_gms])
RETURN IF(CareCalls >= 5, 30, CareCalls * 6) + IF(Weight >= 5000, 25, Weight / 200)
```

---

## 🎨 **Dashboard Design**

### **Executive Dashboard Features:**
- **4 KPI Cards:** Core metrics with conditional formatting
- **Trend Analysis:** Volume vs Performance combo chart
- **Warehouse Performance:** Donut chart with 5-color palette
- **Transport Analysis:** Column chart comparison
- **Dynamic Insights:** Auto-updating business intelligence
- **Risk Indicators:** Real-time alerting system

### **Color Palette:**
```css
Background: #4A154B (Dark Purple)
KPI Cards: Gradient backgrounds
Charts: Professional Gray (#85929E) + Orange (#F39C12)
Text: White (#FFFFFF)
Accents: Multi-color spectrum for categoricals
```

---

## ⚡ **Performance Optimizations**

### **Data Model Optimizations:**
- **Surrogate Keys:** Integer-based relationships
- **Data Types:** Optimized for memory efficiency
- **Calculated Columns:** Minimized for performance
- **Cross-Filter:** Single direction relationships

### **DAX Optimizations:**
- **VAR Usage:** Reduced calculation overhead
- **FILTER vs CALCULATE:** Context-appropriate selection
- **RELATED vs LOOKUPVALUE:** Relationship-based lookups
- **Iterator Functions:** AVERAGEX, SUMX for row context

---

## 📁 **Project Structure**

```
📦 Logistics-Performance-Analytics-Hub/
├── 📊 Data/
│   └── Train.csv (Original dataset)
├── 📋 Documentation/
│   ├── Data-Model-Schema.png
│   ├── DAX-Measures-Guide.pdf
│   └── Dashboard-Screenshots/
├── 🔧 Power-BI-Files/
│   ├── Logistics-Analytics-Hub.pbix
│   └── Data-Model-Template.pbit
└── 📖 README.md
```

---

## 🚀 **Key Business Insights**

### **Critical Findings:**
- **Delivery Performance:** 59.67% on-time delivery rate
- **Performance Decline:** Significant drop from Period 1 (100%) to Period 5 (42%)
- **Transport Efficiency:** Flight mode shows best performance (60%)
- **Customer Satisfaction:** Average 2.99/5 rating indicates improvement opportunities
- **Volume Impact:** Higher shipment volumes correlate with performance decline

### **Actionable Recommendations:**
1. **Investigate Period 5 Performance Drop** - Root cause analysis needed
2. **Optimize Heavy Package Handling** - Weight-based process improvements
3. **Enhance Customer Service** - Address high care call rates (32.61% problem customers)
4. **Warehouse Standardization** - Balance performance across all facilities

---

## 🛠️ **Technical Requirements**

- **Power BI Desktop:** Latest version
- **Data Source:** CSV file support
- **Memory:** 8GB+ recommended for optimal performance
- **Power Query:** M language knowledge for data transformations
- **DAX:** Advanced formula knowledge for custom measures

---

## 📈 **Future Enhancements**

### **Version 2.0 Roadmap:**
- **📅 Date Dimension:** Time intelligence capabilities
- **🔐 Row Level Security:** User-based data access
- **📱 Mobile Optimization:** Responsive dashboard design
- **🤖 Predictive Analytics:** Machine learning integration
- **📊 Real-time Data:** Direct query connections

---

## 🤝 **Contributing**

This project demonstrates **enterprise-level Power BI development** practices. Feel free to:
- Fork and enhance the data model
- Add new DAX measures and calculations  
- Improve dashboard design and UX
- Submit issues and feature requests

---

## 📝 **License**

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 **Author**

**Burak Karagöz**
- Power BI Expert & Data Analytics Specialist
- LinkedIn: [https://www.linkedin.com/in/trburakkaragoz/](https://www.linkedin.com/in/trburakkaragoz/)
- Email: karagozburak.16@gmail.com

---

## 🏆 **Acknowledgments**

Built as part of **advanced Power BI training** to demonstrate:
- Star Schema data modeling best practices
- Advanced DAX programming techniques
- Executive-level dashboard design principles
- Performance optimization strategies

**⭐ If this project helped you learn Power BI, please give it a star!**
