# Claude App Builder - $app Mode Patterns & Examples

**Complete patterns and examples for building general web applications with the $app mode.**

## 📑 TABLE OF CONTENTS

1. [Overview](#1-overview)
2. [Common App Types](#2-common-app-types)
3. [Complete Examples](#3-complete-examples)
4. [Integration Patterns](#4-integration-patterns)

---

## 1. OVERVIEW

### What is $app Mode?

The `$app` mode is for building general web applications that don't fit the specific patterns of chat, analysis, or orchestration modes. Use it for:

- **Dashboards** - Admin panels, analytics dashboards, monitoring tools
- **CRUD Applications** - Todo lists, contact managers, inventory systems
- **Tools & Utilities** - Calculators, converters, generators
- **Content Management** - Blog editors, documentation sites, portfolios
- **E-commerce** - Product catalogs, shopping carts, checkout flows
- **Forms & Workflows** - Multi-step forms, approval workflows, surveys

### Mode Selection
```
User says "dashboard" or "admin panel" → $app
User says "todo app" or "task manager" → $app
User says "calculator" or "converter" → $app
User says "portfolio" or "website" → $app
```

---

## 2. COMMON APP TYPES

### Dashboard Pattern
```jsx
const DashboardApp = () => {
  const [metrics, setMetrics] = useState({
    users: 1234,
    revenue: 45678,
    growth: 12.5,
    active: 89
  });
  
  return (
    <div className="min-h-screen bg-gray-50">
      {/* Header */}
      <header className="bg-white shadow-sm">
        <div className="px-[clamp(1rem,5vw,3rem)] py-[clamp(1rem,2vw,1.5rem)]">
          <h1 className="text-[clamp(1.5rem,3vw,2rem)] font-bold">Dashboard</h1>
        </div>
      </header>
      
      {/* Metrics Grid */}
      <main className="p-[clamp(1rem,5vw,3rem)]">
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-[clamp(1rem,3vw,2rem)]">
          {Object.entries(metrics).map(([key, value]) => (
            <MetricCard key={key} label={key} value={value} />
          ))}
        </div>
      </main>
    </div>
  );
};
```

### CRUD Application Pattern
```jsx
const TodoApp = () => {
  const [todos, setTodos] = useState([]);
  const [filter, setFilter] = useState('all');
  
  const addTodo = (text) => {
    setTodos([...todos, {
      id: Date.now(),
      text,
      completed: false,
      createdAt: new Date()
    }]);
  };
  
  const updateTodo = (id, updates) => {
    setTodos(todos.map(todo => 
      todo.id === id ? { ...todo, ...updates } : todo
    ));
  };
  
  const deleteTodo = (id) => {
    setTodos(todos.filter(todo => todo.id !== id));
  };
  
  return (
    <div className="max-w-[clamp(20rem,90vw,40rem)] mx-auto p-[clamp(1rem,5vw,3rem)]">
      <TodoHeader onAdd={addTodo} />
      <TodoFilters filter={filter} onChange={setFilter} />
      <TodoList 
        todos={todos} 
        filter={filter}
        onUpdate={updateTodo}
        onDelete={deleteTodo}
      />
    </div>
  );
};
```

### Form & Workflow Pattern
```jsx
const MultiStepForm = () => {
  const [currentStep, setCurrentStep] = useState(0);
  const [formData, setFormData] = useState({});
  
  const steps = [
    { id: 'personal', title: 'Personal Info', component: PersonalStep },
    { id: 'contact', title: 'Contact Details', component: ContactStep },
    { id: 'review', title: 'Review', component: ReviewStep }
  ];
  
  const updateData = (stepData) => {
    setFormData({ ...formData, ...stepData });
  };
  
  return (
    <div className="max-w-[clamp(25rem,80vw,50rem)] mx-auto">
      <ProgressIndicator steps={steps} current={currentStep} />
      
      <div className="bg-white rounded-lg shadow-lg p-[clamp(1.5rem,5vw,3rem)]">
        {React.createElement(steps[currentStep].component, {
          data: formData,
          onUpdate: updateData,
          onNext: () => setCurrentStep(Math.min(currentStep + 1, steps.length - 1)),
          onBack: () => setCurrentStep(Math.max(currentStep - 1, 0))
        })}
      </div>
    </div>
  );
};
```

---

## 3. COMPLETE EXAMPLES

### Example 1: Project Management Dashboard

```jsx
/**
 * App: Project Manager | v1.0.0 | Mode: $app
 * Desc: Simple project management dashboard with tasks and team overview
 * Features: Project list, task management, team members, progress tracking
 * Usage: Add projects, assign tasks, track progress
 */

import React, { useState } from 'react';
import { Plus, CheckCircle, Clock, Users, Folder } from 'lucide-react';

export default function ProjectManager() {
  const [projects, setProjects] = useState([
    {
      id: 1,
      name: 'Website Redesign',
      tasks: 12,
      completed: 8,
      team: ['Alice', 'Bob'],
      dueDate: '2024-02-15'
    },
    {
      id: 2,
      name: 'Mobile App',
      tasks: 20,
      completed: 5,
      team: ['Charlie', 'David', 'Eve'],
      dueDate: '2024-03-01'
    }
  ]);
  
  const [showAddProject, setShowAddProject] = useState(false);
  
  const addProject = (project) => {
    setProjects([...projects, {
      ...project,
      id: Date.now(),
      tasks: 0,
      completed: 0
    }]);
    setShowAddProject(false);
  };
  
  return (
    <div className="min-h-screen bg-gray-50">
      {/* Header */}
      <header className="bg-white shadow-sm border-b">
        <div className="max-w-7xl mx-auto px-[clamp(1rem,5vw,3rem)] py-[clamp(1rem,2vw,1.5rem)]">
          <div className="flex items-center justify-between">
            <h1 className="text-[clamp(1.5rem,3vw,2rem)] font-bold text-gray-900">
              Project Manager
            </h1>
            <button
              onClick={() => setShowAddProject(true)}
              className="flex items-center gap-2 px-[clamp(1rem,2vw,1.5rem)] py-[clamp(0.5rem,1vw,0.75rem)] 
                       bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition-colors"
            >
              <Plus className="w-5 h-5" />
              <span className="text-[clamp(0.875rem,1.2vw,1rem)]">New Project</span>
            </button>
          </div>
        </div>
      </header>
      
      {/* Stats Overview */}
      <div className="max-w-7xl mx-auto px-[clamp(1rem,5vw,3rem)] py-[clamp(1.5rem,3vw,2rem)]">
        <div className="grid grid-cols-1 md:grid-cols-4 gap-[clamp(1rem,3vw,2rem)]">
          <StatCard 
            icon={Folder} 
            label="Total Projects" 
            value={projects.length}
            color="blue"
          />
          <StatCard 
            icon={CheckCircle} 
            label="Tasks Completed" 
            value={projects.reduce((acc, p) => acc + p.completed, 0)}
            color="green"
          />
          <StatCard 
            icon={Clock} 
            label="Tasks Pending" 
            value={projects.reduce((acc, p) => acc + (p.tasks - p.completed), 0)}
            color="orange"
          />
          <StatCard 
            icon={Users} 
            label="Team Members" 
            value={new Set(projects.flatMap(p => p.team)).size}
            color="purple"
          />
        </div>
      </div>
      
      {/* Projects Grid */}
      <div className="max-w-7xl mx-auto px-[clamp(1rem,5vw,3rem)] pb-[clamp(2rem,5vw,4rem)]">
        <h2 className="text-[clamp(1.25rem,2vw,1.5rem)] font-semibold mb-[clamp(1rem,2vw,1.5rem)]">
          Active Projects
        </h2>
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-[clamp(1rem,3vw,2rem)]">
          {projects.map(project => (
            <ProjectCard key={project.id} project={project} />
          ))}
        </div>
      </div>
      
      {/* Add Project Modal */}
      {showAddProject && (
        <AddProjectModal 
          onAdd={addProject}
          onClose={() => setShowAddProject(false)}
        />
      )}
    </div>
  );
}

// Component implementations...
const StatCard = ({ icon: Icon, label, value, color }) => {
  const colors = {
    blue: 'bg-blue-100 text-blue-600',
    green: 'bg-green-100 text-green-600',
    orange: 'bg-orange-100 text-orange-600',
    purple: 'bg-purple-100 text-purple-600'
  };
  
  return (
    <div className="bg-white rounded-lg shadow p-[clamp(1rem,3vw,1.5rem)]">
      <div className="flex items-center justify-between">
        <div>
          <p className="text-[clamp(0.75rem,1vw,0.875rem)] text-gray-500">{label}</p>
          <p className="text-[clamp(1.5rem,3vw,2rem)] font-bold mt-1">{value}</p>
        </div>
        <div className={`p-3 rounded-lg ${colors[color]}`}>
          <Icon className="w-6 h-6" />
        </div>
      </div>
    </div>
  );
};

const ProjectCard = ({ project }) => {
  const progress = (project.completed / project.tasks) * 100;
  
  return (
    <div className="bg-white rounded-lg shadow-lg p-[clamp(1rem,3vw,1.5rem)] hover:shadow-xl transition-shadow">
      <h3 className="text-[clamp(1rem,1.5vw,1.25rem)] font-semibold mb-3">{project.name}</h3>
      
      <div className="space-y-3">
        <div>
          <div className="flex justify-between text-sm text-gray-600 mb-1">
            <span>Progress</span>
            <span>{project.completed}/{project.tasks} tasks</span>
          </div>
          <div className="w-full bg-gray-200 rounded-full h-2">
            <div 
              className="bg-blue-500 h-2 rounded-full transition-all duration-300"
              style={{ width: `${progress}%` }}
            />
          </div>
        </div>
        
        <div className="flex items-center gap-2 text-sm text-gray-600">
          <Users className="w-4 h-4" />
          <span>{project.team.join(', ')}</span>
        </div>
        
        <div className="flex items-center gap-2 text-sm text-gray-600">
          <Clock className="w-4 h-4" />
          <span>Due {project.dueDate}</span>
        </div>
      </div>
    </div>
  );
};
```

### Example 2: E-commerce Product Catalog

```jsx
/**
 * App: Product Catalog | v1.0.0 | Mode: $app
 * Desc: E-commerce product browsing with filters and cart
 * Features: Product grid, category filters, search, shopping cart
 * Usage: Browse products, filter by category, add to cart
 */

import React, { useState, useMemo } from 'react';
import { Search, ShoppingCart, Star, Filter } from 'lucide-react';

export default function ProductCatalog() {
  const [products] = useState([
    { id: 1, name: 'Wireless Headphones', price: 79.99, category: 'Electronics', rating: 4.5, image: '🎧' },
    { id: 2, name: 'Smart Watch', price: 199.99, category: 'Electronics', rating: 4.8, image: '⌚' },
    { id: 3, name: 'Yoga Mat', price: 29.99, category: 'Fitness', rating: 4.3, image: '🧘' },
    { id: 4, name: 'Coffee Maker', price: 89.99, category: 'Home', rating: 4.6, image: '☕' },
    // Add more products...
  ]);
  
  const [cart, setCart] = useState([]);
  const [searchTerm, setSearchTerm] = useState('');
  const [selectedCategory, setSelectedCategory] = useState('all');
  const [showCart, setShowCart] = useState(false);
  
  const categories = ['all', ...new Set(products.map(p => p.category))];
  
  const filteredProducts = useMemo(() => {
    return products.filter(product => {
      const matchesSearch = product.name.toLowerCase().includes(searchTerm.toLowerCase());
      const matchesCategory = selectedCategory === 'all' || product.category === selectedCategory;
      return matchesSearch && matchesCategory;
    });
  }, [products, searchTerm, selectedCategory]);
  
  const addToCart = (product) => {
    setCart(prev => {
      const existing = prev.find(item => item.id === product.id);
      if (existing) {
        return prev.map(item => 
          item.id === product.id 
            ? { ...item, quantity: item.quantity + 1 }
            : item
        );
      }
      return [...prev, { ...product, quantity: 1 }];
    });
  };
  
  const cartTotal = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
  const cartCount = cart.reduce((sum, item) => sum + item.quantity, 0);
  
  return (
    <div className="min-h-screen bg-gray-50">
      {/* Header */}
      <header className="bg-white shadow-sm sticky top-0 z-10">
        <div className="max-w-7xl mx-auto px-[clamp(1rem,5vw,3rem)] py-[clamp(1rem,2vw,1.5rem)]">
          <div className="flex items-center justify-between gap-4">
            <h1 className="text-[clamp(1.5rem,3vw,2rem)] font-bold">Shop</h1>
            
            {/* Search */}
            <div className="flex-1 max-w-md">
              <div className="relative">
                <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
                <input
                  type="text"
                  value={searchTerm}
                  onChange={(e) => setSearchTerm(e.target.value)}
                  placeholder="Search products..."
                  className="w-full pl-10 pr-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                />
              </div>
            </div>
            
            {/* Cart */}
            <button
              onClick={() => setShowCart(!showCart)}
              className="relative p-2 text-gray-600 hover:text-gray-900"
            >
              <ShoppingCart className="w-6 h-6" />
              {cartCount > 0 && (
                <span className="absolute -top-1 -right-1 bg-red-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center">
                  {cartCount}
                </span>
              )}
            </button>
          </div>
        </div>
      </header>
      
      <div className="max-w-7xl mx-auto px-[clamp(1rem,5vw,3rem)] py-[clamp(2rem,4vw,3rem)]">
        {/* Filters */}
        <div className="mb-6">
          <div className="flex items-center gap-4 flex-wrap">
            <Filter className="w-5 h-5 text-gray-600" />
            {categories.map(category => (
              <button
                key={category}
                onClick={() => setSelectedCategory(category)}
                className={`px-4 py-2 rounded-lg capitalize transition-colors ${
                  selectedCategory === category
                    ? 'bg-blue-500 text-white'
                    : 'bg-white text-gray-700 hover:bg-gray-100'
                }`}
              >
                {category}
              </button>
            ))}
          </div>
        </div>
        
        {/* Products Grid */}
        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-[clamp(1rem,3vw,2rem)]">
          {filteredProducts.map(product => (
            <ProductCard 
              key={product.id} 
              product={product} 
              onAddToCart={addToCart}
            />
          ))}
        </div>
      </div>
      
      {/* Cart Sidebar */}
      {showCart && (
        <CartSidebar 
          cart={cart}
          total={cartTotal}
          onClose={() => setShowCart(false)}
          onUpdateQuantity={(id, quantity) => {
            if (quantity === 0) {
              setCart(cart.filter(item => item.id !== id));
            } else {
              setCart(cart.map(item => 
                item.id === id ? { ...item, quantity } : item
              ));
            }
          }}
        />
      )}
    </div>
  );
}

const ProductCard = ({ product, onAddToCart }) => (
  <div className="bg-white rounded-lg shadow hover:shadow-lg transition-shadow">
    <div className="p-8 text-center text-6xl bg-gray-100 rounded-t-lg">
      {product.image}
    </div>
    <div className="p-4">
      <h3 className="font-semibold text-[clamp(1rem,1.5vw,1.25rem)]">{product.name}</h3>
      <div className="flex items-center gap-1 my-2">
        {[...Array(5)].map((_, i) => (
          <Star 
            key={i} 
            className={`w-4 h-4 ${
              i < Math.floor(product.rating) 
                ? 'fill-yellow-400 text-yellow-400' 
                : 'text-gray-300'
            }`} 
          />
        ))}
        <span className="text-sm text-gray-600 ml-1">{product.rating}</span>
      </div>
      <div className="flex items-center justify-between mt-4">
        <span className="text-[clamp(1.25rem,2vw,1.5rem)] font-bold">${product.price}</span>
        <button
          onClick={() => onAddToCart(product)}
          className="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition-colors"
        >
          Add to Cart
        </button>
      </div>
    </div>
  </div>
);
```

---

## 4. INTEGRATION PATTERNS

### State Management for Apps
```jsx
// For complex app state, use useReducer
const appReducer = (state, action) => {
  switch (action.type) {
    case 'SET_USER':
      return { ...state, user: action.payload };
    case 'UPDATE_SETTINGS':
      return { ...state, settings: { ...state.settings, ...action.payload } };
    case 'ADD_NOTIFICATION':
      return { ...state, notifications: [...state.notifications, action.payload] };
    case 'REMOVE_NOTIFICATION':
      return { ...state, notifications: state.notifications.filter(n => n.id !== action.payload) };
    default:
      return state;
  }
};

// Usage
const [state, dispatch] = useReducer(appReducer, initialState);
```

### Data Persistence Pattern
```jsx
// Session-only persistence (no localStorage)
const useAppData = (key, initialValue) => {
  const [data, setData] = useState(initialValue);
  
  // Auto-save to component state
  const updateData = useCallback((newData) => {
    setData(newData);
    // Could trigger auto-save to backend here
  }, []);
  
  return [data, updateData];
};
```

### Common App Components
```jsx
// Reusable layout wrapper
const AppLayout = ({ children, title, actions }) => (
  <div className="min-h-screen bg-gray-50">
    <header className="bg-white shadow-sm">
      <div className="max-w-7xl mx-auto px-[clamp(1rem,5vw,3rem)] py-[clamp(1rem,2vw,1.5rem)]">
        <div className="flex items-center justify-between">
          <h1 className="text-[clamp(1.5rem,3vw,2rem)] font-bold">{title}</h1>
          <div className="flex gap-2">{actions}</div>
        </div>
      </div>
    </header>
    <main className="max-w-7xl mx-auto px-[clamp(1rem,5vw,3rem)] py-[clamp(2rem,4vw,3rem)]">
      {children}
    </main>
  </div>
);

// Empty state component
const EmptyState = ({ icon: Icon, title, description, action }) => (
  <div className="text-center py-12">
    <Icon className="w-12 h-12 text-gray-400 mx-auto mb-4" />
    <h3 className="text-lg font-medium text-gray-900 mb-2">{title}</h3>
    <p className="text-gray-500 mb-4">{description}</p>
    {action}
  </div>
);
```

---

## Best Practices

1. **Use fluid responsive design** for all sizing
2. **Implement proper loading states** for all async operations
3. **Include empty states** when no data exists
4. **Add error boundaries** for resilience
5. **Use semantic HTML** for accessibility
6. **Keep components modular** and reusable
7. **Optimize for performance** with React.memo and useCallback

---

*Build complete web applications with the $app mode. Focus on user experience, fluid design, and clean architecture.*