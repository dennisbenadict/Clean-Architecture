# 🚀 CLEAN ARCHITECTURE

# 🔁 FULL SYSTEM FLOW

**CLIENT → API → APPLICATION → DOMAIN → INFRASTRUCTURE → DB**

```
       API / Presentation
              ↓
         Application
              ↓
           Domain
              ↑
        Infrastructure
```

## 🔥 LAYER ORDER (Innermost → Outermost)

1️⃣ **DOMAIN** *(Innermost — Core Rules)*  
2️⃣ **APPLICATION** *(Use Cases)*  
3️⃣ **INFRASTRUCTURE** *(Implementations)*  
4️⃣ **API** *(Outermost — Presentation)*  

Inner layers must **never depend on outer layers**.

---

# 1️⃣ DOMAIN (Innermost Layer)

### **What Domain Is**
- Entities, Value Objects, Core Business Rules.

### **What Domain Can Reference**
- **Nothing**

### **Who Can Reference Domain**
- Application  
- Infrastructure  
- API (allowed but not recommended)

### **Core Rules**
- Domain depends on **no one**.  
- Domain contains **pure business rules only**.  
- Domain **never calls** Application or Infrastructure.

---

# 2️⃣ APPLICATION (Use Case Layer)

### **What Application Is**
- Use Cases, Services, Commands, Queries.  
- Defines **interfaces (ports)** that Infrastructure must implement.

### **What Application Can Reference**
- **Domain only**

### **Who Can Reference Application**
- API  
- Infrastructure  

### **Core Rules**
- Application depends only on **Domain**.  
- Application defines **interfaces** for Infrastructure implementations.  
- Application must not depend on Infrastructure or external frameworks.

### **Communication**
- Application → Domain  
- Application → Infrastructure (via interfaces)

---

# 3️⃣ INFRASTRUCTURE (Implementation Layer)

### **What Infrastructure Is**
- Database logic  
- Repository implementations  
- External service calls  
- File storage, messaging, etc.

### **What Infrastructure Can Reference**
- **Application**  
- **Domain**

### **Who Can Reference Infrastructure**
- **API (only in Program.cs)** for DI wiring  
- No other layer should reference Infrastructure for logic

### **Core Rules**
- Infrastructure implements interfaces defined in Application.  
- Infrastructure must not contain business rules.  
- Infrastructure must not be called directly by API or Domain.

### **Communication**
- Infrastructure → Application (via interface implementations)  
- Infrastructure → DB / external systems

---

# 4️⃣ API (Outermost Layer)

### **What API Is**
- Controllers, Endpoints, Presentation logic.

### **What API Can Reference**
- **Application**  
- **Infrastructure** (optional, only for DI wiring)

### **Who References API**
- No layer references API.

### **Core Rules**
- API must call **Application only**.  
- API must not call Infrastructure for business logic.  
- API must not access Domain logic directly.

### **Communication**
- API → Application

---

# 🔄 RUNTIME FLOW (Simple)

1. **API receives request**  
2. **Application handles use case**  
3. **Domain executes rules**  
4. **Application calls Infrastructure (via interface)**  
5. **Infrastructure talks to DB**  
6. **Response returns upward**

---

#***__BY DENNIS BENADICT__***       
