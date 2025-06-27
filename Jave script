/* ============================================================================ /
/ PLAMPAY - COMPLETE JAVASCRIPT CODE /
/ Investment Platform Frontend & Backend JavaScript /
/ ============================================================================ */

// ============================================================================
// BANK ACCOUNT DETAILS
// ============================================================================

const bankDetails = {
    accountName: "Plampay",
    accountHolder: "Theresa Chisom Chukwu",
    accountNumber: "8122977435"
};

// ============================================================================
// FRONTEND JAVASCRIPT CODE
// ============================================================================

// Basic Investment Calculator Functions
function validateAmount(amount) {
    const num = parseFloat(amount);
    if (isNaN(num) || num <= 0) {
        return "Please enter a valid amount";
    }
    if (num < 10) {
        return "Minimum investment is $10";
    }
    if (num > 50000) {
        return "Maximum investment is $50,000";
    }
    return null;
}

// Investment return calculations
function calculateInvestmentReturn(amount, plan) {
    const rates = {
        "1week": 0.15,
        "3week": 0.25
    };

    const rate = rates[plan] || 0;
    const principal = parseFloat(amount) || 0;
    const returns = principal * rate;
    const total = principal + returns;

    return {
        principal: principal.toFixed(2),
        returns: returns.toFixed(2),
        total: total.toFixed(2),
        percentage: ((rate * 100).toFixed(0) + '%'),
        days: plan === '1week' ? 7 : 21
    };
}

// Currency formatting utility
function formatCurrency(amount) {
    const num = parseFloat(amount) || 0;
    return new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD',
        minimumFractionDigits: 2,
        maximumFractionDigits: 2
    }).format(num);
}

// Date formatting utility
function formatDate(dateString) {
    const date = new Date(dateString);
    return date.toLocaleDateString('en-US', {
        year: 'numeric',
        month: 'short',
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
    });
}

// Relative time formatting
function formatRelativeTime(dateString) {
    const date = new Date(dateString);
    const now = new Date();
    const diffMs = now - date;
    const diffMins = Math.floor(diffMs / 60000);
    const diffHours = Math.floor(diffMs / 3600000);
    const diffDays = Math.floor(diffMs / 86400000);

    if (diffMins < 1) return 'Just now';
    if (diffMins < 60) return `${diffMins}m ago`;
    if (diffHours < 24) return `${diffHours}h ago`;
    if (diffDays < 7) return `${diffDays}d ago`;
    return formatDate(dateString);
}

// Investment maturity calculation
function calculateMaturityDate(startDate, plan) {
    const start = new Date(startDate);
    const days = plan === '1week' ? 7 : 21;
    const maturity = new Date(start.getTime() + (days * 24 * 60 * 60 * 1000));
    return maturity;
}

// Days until maturity
function getDaysUntilMaturity(maturityDate) {
    const now = new Date();
    const maturity = new Date(maturityDate);
    const diffMs = maturity - now;
    const diffDays = Math.ceil(diffMs / (24 * 60 * 60 * 1000));
    return Math.max(0, diffDays);
}

// Simple notification system
function showNotification(message, type = 'info', duration = 5000) {
    const notification = document.createElement('div');
    notification.className = `notification notification-${type}`;

    const content = document.createElement('div');
    content.innerHTML = `
        <div class="notification-title">${getNotificationTitle(type)}</div>
        <div class="notification-message">${message}</div>
    `;
    notification.appendChild(content);

    Object.assign(notification.style, {
        position: 'fixed',
        top: '20px',
        right: '20px',
        padding: '1rem 1.5rem',
        backgroundColor: getNotificationColor(type),
        color: 'white',
        borderRadius: '0.5rem',
        boxShadow: '0 10px 15px -3px rgba(0, 0, 0, 0.1)',
        zIndex: '1000',
        fontSize: '0.875rem',
        fontWeight: '500',
        maxWidth: '350px',
        minWidth: '250px',
        animation: 'slideIn 0.3s ease-out'
    });

    document.body.appendChild(notification);

    setTimeout(() => {
        notification.style.animation = 'slideOut 0.3s ease-in forwards';
        setTimeout(() => {
            if (notification.parentNode) {
                notification.remove();
            }
        }, 300);
    }, duration);

    notification.addEventListener('click', () => {
        notification.remove();
    });
}

function getNotificationTitle(type) {
    const titles = {
        'success': 'Success',
        'error': 'Error',
        'warning': 'Warning',
        'info': 'Information'
    };
    return titles[type] || 'Notification';
}

function getNotificationColor(type) {
    const colors = {
        'success': '#22C55E',
        'error': '#EF4444',
        'warning': '#F59E0B',
        'info': '#3B82F6'
    };
    return colors[type] || '#3B82F6';
}

// Form validation utilities
function validateEmail(email) {
    const emailRegex = /^[^\\s@]+@[^\\s@]+\\.[^\\s@]+$/;
    return emailRegex.test(email);
}

function validatePhoneNumber(phone) {
    const phoneRegex = /^\\+?[\\d\\s-]{10,}$/;
    return phoneRegex.test(phone.replace(/\\s/g, ''));
}

function validatePassword(password) {
    if (password.length < 8) return \"Password must be at least 8 characters long\";
    if (!/[A-Z]/.test(password)) return \"Password must contain at least one uppercase letter\";
    if (!/[a-z]/.test(password)) return \"Password must contain at least one lowercase letter\";
    if (!/\\d/.test(password)) return \"Password must contain at least one number\";
    return null;
}

// Local storage utilities
function saveToLocalStorage(key, data) {
    try {
        localStorage.setItem(key, JSON.stringify(data));
    } catch (error) {
        console.warn('Failed to save to localStorage:', error);
    }
}

function loadFromLocalStorage(key, defaultValue = null) {
    try {
        const item = localStorage.getItem(key);
        return item ? JSON.parse(item) : defaultValue;
    } catch (error) {
        console.warn('Failed to load from localStorage:', error);
        return defaultValue;
    }
}

function removeFromLocalStorage(key) {
    try {
        localStorage.removeItem(key);
    } catch (error) {
        console.warn('Failed to remove from localStorage:', error);
    }
}

// Theme management
function toggleTheme() {
    const currentTheme = document.documentElement.getAttribute('data-theme');
    const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
    document.documentElement.setAttribute('data-theme', newTheme);
    saveToLocalStorage('theme', newTheme);
    showNotification(`Switched to ${newTheme} theme`, 'info', 2000);
}

function initializeTheme() {
    const savedTheme = loadFromLocalStorage('theme', 'light');
    const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
    const theme = savedTheme || (prefersDark ? 'dark' : 'light');
    document.documentElement.setAttribute('data-theme', theme);
}

// Call this on page load
function initializePage() {
    initializeTheme();
    showNotification('Welcome to PlamPay! Your secure investment platform.', 'success', 3000);
}
