# 🚀 BIXA Database Migration Tool v3.3

[![Python](https://img.shields.io/badge/Python-3.7%2B-blue.svg)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey.svg)](README.md)

Professional database migration tool with modern GUI, designed to safely and efficiently migrate data from legacy hosting systems to Laravel 11.

## ✨ Key Features

### 🔄 Data Migration
- **Multiple data sources**: Support direct database connection or SQL file import
- **Comprehensive migration**: Migrate users, admins, accounts, tickets, SSL certificates
- **Batch processing**: Process data in batches for optimal performance
- **Auto-retry**: Automatic retry on errors

### 🔐 Security
- **Password generation**: Automatically generate strong passwords for all users
- **Bcrypt hashing**: Password encryption using bcrypt (10 rounds)
- **Secure export**: Security warnings when exporting sensitive data
- **Activity logging**: Complete logging of all activities

### 📧 Automated Email
- **SMTP integration**: Full support for all SMTP providers
- **Batch email**: Send emails in batches with customizable delay
- **Customizable templates**: Email templates can be customized
- **Delivery tracking**: Track email sending status

### 📊 Monitoring & Reporting
- **Real-time progress**: Real-time progress tracking
- **Detailed dashboard**: Detailed statistics by category
- **Export reports**: Export reports in multiple formats (JSON, CSV, TXT)
- **Advanced logging**: System logs with multiple levels (INFO, WARNING, ERROR, SUCCESS)

### 🎨 Modern Interface
- **Dark theme**: Modern dark interface, easy on the eyes
- **Responsive design**: Automatically adjusts to window size
- **Modern navigation**: Intuitive sidebar navigation
- **Color-coded status**: Clear color coding for different statuses

## 📋 System Requirements

### Python
- **Version**: Python 3.7 or higher
- **Packages**: Tool will automatically install required packages

### Database
- **Source**: MySQL/MariaDB (old database)
- **Target**: MySQL/MariaDB (Laravel 11 database)
- **Permissions**: SELECT on source, INSERT/UPDATE on target

### Email (Optional)
- **SMTP server**: Gmail, Outlook, or other SMTP server
- **Authentication**: Username/password or App Password

## 🚀 Installation and Running

### 1. Download
```bash
# Clone repository or download migration.py file
wget https://your-repo/migration.py
# or
git clone https://your-repo/bixa-migration-tool.git
cd bixa-migration-tool
```

### 2. Run Directly
```bash
python migration.py
```

The tool will automatically:
- Check and install required dependencies
- Launch the graphical interface
- Display dependency status

### 3. Auto Dependencies
Tool will automatically install:
- `mysql-connector-python`: MySQL connection
- `PyMySQL`: Alternative MySQL connector
- `bcrypt`: Password hashing

## 📖 User Guide

### Step 1: Configure Data Source

#### Option A: Database Connection
1. Open **"⚙️ Configuration"** tab
2. Select **"Connect to Database Directly"**
3. Fill in **Old Database (Source)** information:
   - Host: IP/hostname of old database
   - Port: 3306 (default)
   - Database: Old database name
   - Username: User with SELECT permissions
   - Password: Database password
4. Click **"🔍 Test Connection"** to verify

#### Option B: SQL File Import
1. Select **"Import from SQL File"**
2. Click **"📁 Browse"** to select SQL dump file
3. Click **"🔍 Test SQL File"** to parse and check data
4. Tool will display statistics of found data

### Step 2: Configure Target Database
1. Fill in **New Database (Target)** information:
   - Host: IP/hostname of Laravel database
   - Port: 3306 (default)
   - Database: Laravel database name
   - Username: User with INSERT/UPDATE permissions
   - Password: Database password
2. Click **"🔍 Test Connection"** to verify

### Step 3: Configure Migration Settings
- **Batch Size**: Number of records processed per batch (default: 100)
- **User Password Length**: Password length for users (default: 12)
- **Admin Password Length**: Password length for admins (default: 14)

### Step 4: Run Migration
1. Switch to **"🚀 Migration"** tab
2. Click **"🚀 Start Full Migration"**
3. Monitor progress through progress bars
4. View detailed logs in **"📝 Logs"** tab

### Step 5: Configure Email (Optional)
1. Open **"📧 Email Setup"** tab
2. Configure SMTP settings:
   - **SMTP Host**: smtp.gmail.com (for Gmail)
   - **Port**: 587 (for TLS)
   - **Username**: Email address
   - **Password**: App password (not regular password)
   - **From Email**: Sender email
   - **From Name**: Display name
3. Click **"🧪 Test SMTP Connection"**
4. Adjust Email Settings:
   - **Batch Size**: Number of emails sent per batch
   - **Delay**: Delay time between batches (seconds)

### Step 6: Send Password Emails
1. Click **"📧 Send All Password Emails"**
2. Confirm in dialog
3. Monitor email sending progress

### Step 7: Check Results
1. View statistics in **"📊 Dashboard"** tab
2. Export report: **"📄 Export Report"**
3. Export password list: **"🔑 Export Passwords"** (handle with care!)

## ⚙️ Advanced Configuration

### Database Tables Mapping

#### Source Tables (Old Database)
```sql
is_user     -> users (role: 'user')
is_admin    -> users (role: 'admin')  
is_account  -> accounts
is_ticket   -> tickets
is_ssl      -> ssl_certificates
```

#### Laravel 11 Target Schema
```sql
users:
- id (auto increment)
- name (from user_name/admin_name)
- email (from user_email/admin_email)
- password (bcrypt hashed)
- role ('user' or 'admin')
- email_verified_at
- created_at (from user_date/admin_date)
- updated_at
```

### SMTP Configuration Examples

#### Gmail
```
Host: smtp.gmail.com
Port: 587
Username: your-email@gmail.com
Password: your-app-password (16 characters)
```

#### Outlook/Hotmail
```
Host: smtp-mail.outlook.com
Port: 587
Username: your-email@outlook.com
Password: your-password
```

#### Custom SMTP
```
Host: your-smtp-server.com
Port: 587/465/25
Username: your-username
Password: your-password
```

### Config File Format
Tool can save/load config in JSON format:
```json
{
  "source_type": "database",
  "old_database": {
    "host": "localhost",
    "port": "3306",
    "database": "old_hosting_db",
    "username": "user",
    "password": "password"
  },
  "new_database": {
    "host": "localhost", 
    "port": "3306",
    "database": "laravel_db",
    "username": "user",
    "password": "password"
  },
  "smtp": {
    "host": "smtp.gmail.com",
    "port": "587",
    "username": "admin@yoursite.com",
    "password": "app-password",
    "from_email": "admin@yoursite.com",
    "from_name": "Migration Tool"
  },
  "settings": {
    "batch_size": "100",
    "user_pwd_length": "12", 
    "admin_pwd_length": "14",
    "email_batch_size": "50",
    "email_delay": "2"
  }
}
```

## 🔒 Security

### Password Security
- **Generation**: Uses Python's `secrets` module
- **Character set**: Letters, numbers, and special characters (!@#$%^&*)
- **Hashing**: Bcrypt with 10 rounds salt
- **Storage**: Plain text only stored in memory, export has security warnings

### Data Protection
- **Database connections**: Uses parameterized queries
- **Log files**: Do not contain passwords
- **Export files**: Clear security warnings
- **Memory**: Clear password data after sending emails

### Network Security
- **SMTP**: Supports TLS/SSL encryption
- **Database**: Connection over secure ports
- **No data transmission**: Tool runs locally, no data sent elsewhere

## 🐛 Troubleshooting

### Dependencies Issues
```bash
# If auto-install fails, install manually:
pip install mysql-connector-python PyMySQL bcrypt

# Or with Python 3:
pip3 install mysql-connector-python PyMySQL bcrypt
```

### Database Connection Issues
- **Check firewall**: Ensure port 3306 is open
- **Check privileges**: User needs appropriate permissions
- **Check MySQL version**: Tool supports MySQL 5.7+
- **Test with MySQL client**: Try connecting with mysql command line

### Email Issues
- **Gmail**: Must use App Password, not regular password
- **2FA**: If 2FA is enabled, App Password is mandatory
- **Firewall**: Check if port 587/465 is blocked
- **Rate limiting**: Reduce batch size and increase delay

### Migration Issues
- **Large datasets**: Increase batch size if database is powerful
- **Memory issues**: Reduce batch size if running low on RAM
- **Timeout**: Check connection timeout settings
- **Duplicate data**: Tool automatically skips duplicate emails

### Performance Tips
- **Database**: Create indexes on email columns
- **Network**: Run tool close to database server
- **Resources**: Ensure sufficient RAM and CPU
- **Batch size**: Adjust according to hardware capabilities

## 📊 Supported Data Types

### Users Migration
- ✅ User accounts (is_user table)
- ✅ Admin accounts (is_admin table)  
- ✅ Email addresses (validation included)
- ✅ User status (active/inactive)
- ✅ Registration dates
- ✅ Password generation and hashing
- ✅ Hosting accounts (is_account)
- ✅ Support tickets (is_ticket)
- ✅ SSL certificates (is_ssl)


## 📞 Support

### Documentation
- **GitHub**: Bixacloud/bixa
- **Telegram**: @bixacloud

### Bug Reports
When reporting bugs, please provide:
1. **Error message**: Copy full error from logs
2. **Environment**: OS, Python version
3. **Database info**: MySQL version, table structure
4. **Steps to reproduce**: Steps leading to the error
5. **Log files**: Attach migration.log file

### Feature Requests
- Create issue on GitHub with "enhancement" label
- Describe the needed feature in detail
- Explain use case and benefits

## 📄 License

MIT License - see LICENSE file for details.

## 🚀 Changelog

### v1.0 (Current)
- ✅ Real SQL file parsing implementation
- ✅ Fixed user migration with actual database operations
- ✅ Improved error handling and logging
- ✅ Enhanced UI with progress tracking
- ✅ Auto-dependency installation

---

**⚠️ Important Note**: Always backup your database before running migration! This tool modifies data and cannot be undone.

**🎯 Best Practice**: Test with a small sample before running full-scale migration.

**📞 Support**: Contact via Telegram @bixacloud if you need assistance.