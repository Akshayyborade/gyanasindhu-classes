# Testing Guide - ज्ञानसिंधू क्लासेस App

## 🧪 How to Test the New Validations

### Prerequisites
- Open the app at: https://akshayyborade.github.io/gyanasindhu-classes/app.html
- Login as Admin with password: `Capital@123`

---

## 1️⃣ Student Form Validation Tests

### Test 1: Add Student with Valid Data
**Steps:**
1. Go to **Students Management**
2. Click **Add Student**
3. Fill in:
   - Name: `Test Student`
   - Father Name: `Test Father`
   - Phone: `9876543210` ✅ (valid)
   - Class: `10`
   - Username: `teststudent` ✅ (valid)
   - Password: `Test@123` ✅ (valid - has uppercase, lowercase, number)
   - Admission Date: Today's date
   - Fee Amount: `10000`
   - Fee Paid: `5000`
4. Click **Save**

**Expected Result:** 
- ✅ Loading spinner appears briefly
- ✅ Success toast: "Student added successfully"
- ✅ Fee Status auto-set to "partial"
- ✅ Student appears in table

---

### Test 2: Invalid Phone Number
**Steps:**
1. Click **Add Student**
2. Enter Phone: `123456789` (9 digits only)
3. Fill other required fields
4. Click **Save**

**Expected Result:**
- ❌ Red error message appears below phone field
- ❌ Error: "Invalid phone number. Must be 10 digits starting with 6-9"
- ❌ Form does NOT submit

**Alternative Tests:**
- Phone: `512345678` → Error (starts with 5, not 6-9)
- Phone: `98765432109` → Error (11 digits)
- Phone: `abcd123456` → Error (contains letters)

---

### Test 3: Invalid Username
**Steps:**
1. Click **Add Student**
2. Enter Username: `ab` (only 2 characters)
3. Fill other fields
4. Click **Save**

**Expected Result:**
- ❌ Red error: "Username must be 3-20 characters (letters, numbers, underscore only)"

**Alternative Tests:**
- Username: `test user` → Error (contains space)
- Username: `test@123` → Error (contains special char @)
- Username: `verylongusernamethatexceeds20chars` → Error (too long)

---

### Test 4: Weak Password
**Steps:**
1. Click **Add Student**
2. Enter Password: `test123` (no uppercase)
3. Fill other fields
4. Click **Save**

**Expected Result:**
- ❌ Red error: "Password must contain at least one uppercase letter"

**Alternative Weak Passwords:**
- `TEST123` → Error: "must contain at least one lowercase letter"
- `TestAbc` → Error: "must contain at least one number"
- `Test1` → Error: "Password must be at least 6 characters"

---

### Test 5: Duplicate Username
**Steps:**
1. Add a student with username: `duplicate123`
2. Try to add another student with username: `duplicate123`
3. Click **Save**

**Expected Result:**
- ❌ Red error: "Username already exists"

---

### Test 6: Fee Overpayment Prevention
**Steps:**
1. Click **Add Student**
2. Enter Fee Amount: `10000`
3. Enter Fee Paid: `15000` (more than amount)
4. Click outside the Fee Paid field (or press Tab)

**Expected Result:**
- ❌ Red error: "Fee paid cannot exceed total fee amount"
- ✅ Fee Paid auto-corrected to `10000`

---

### Test 7: Fee Status Auto-Calculation
**Steps:**
1. Click **Add Student**
2. Enter Fee Amount: `10000`
3. Enter Fee Paid: `0` → Fee Status should show "Pending"
4. Change Fee Paid to: `5000` → Fee Status should change to "Partial"
5. Change Fee Paid to: `10000` → Fee Status should change to "Paid"

**Expected Result:**
- ✅ Fee Status dropdown updates automatically as you type

---

### Test 8: Edit Student (Username Exclusion)
**Steps:**
1. Edit existing student "आनंद पाटील" (username: `anand`)
2. Keep username as `anand` (no change)
3. Update some other field (like phone)
4. Click **Update**

**Expected Result:**
- ✅ Should save successfully (doesn't flag own username as duplicate)

---

## 2️⃣ Teacher Form Validation Tests

### Test 9: Add Teacher with Valid Data
**Steps:**
1. Go to **Teachers Management**
2. Click **Add Teacher**
3. Fill in:
   - Name: `Test Teacher`
   - Phone: `9988776655` ✅
   - Subject: `Mathematics`
   - Username: `testteacher` ✅
   - Password: `Teacher@123` ✅
   - Join Date: Today
   - Assigned Classes: `9,10,11-science`
4. Click **Save**

**Expected Result:**
- ✅ Loading spinner appears
- ✅ Success toast
- ✅ Teacher appears in table

---

### Test 10: Teacher Form Validations
Repeat Tests 2-5 for Teacher form (same validation rules apply)

---

## 3️⃣ Attendance Validation Tests

### Test 11: Mark Attendance (First Time)
**Steps:**
1. Go to **Attendance**
2. Select Date: `2024-01-20`
3. Select Class: `10`
4. Click **Load Students**
5. Mark some present/absent
6. Click **Save Attendance**

**Expected Result:**
- ✅ Loading spinner appears
- ✅ Success toast
- ✅ Attendance saved

---

### Test 12: Duplicate Attendance Prevention
**Steps:**
1. Try to mark attendance again for same date (`2024-01-20`) and class (`10`)
2. Click **Load Students**
3. Mark attendance
4. Click **Save Attendance**

**Expected Result:**
- ❌ Error toast: "Attendance for this class on this date already exists"
- ❌ Attendance NOT saved

---

## 4️⃣ Marks Validation Tests

### Test 13: Add Marks (First Time)
**Steps:**
1. Go to **Marks Management**
2. Select Class: `10`
3. Enter Test Name: `Unit Test 1`
4. Enter Subject: `Mathematics`
5. Enter Total Marks: `100`
6. Select Date
7. Click **Load Students**
8. Enter marks for each student
9. Click **Save Marks**

**Expected Result:**
- ✅ Loading spinner appears
- ✅ Success toast
- ✅ Marks saved

---

### Test 14: Duplicate Marks Prevention
**Steps:**
1. Try to add marks again for:
   - Test: `Unit Test 1`
   - Class: `10`
   - Subject: `Mathematics`
2. Click **Save Marks**

**Expected Result:**
- ❌ Error toast: "Marks for this test, class, and subject already exist"
- ❌ Marks NOT saved

---

## 5️⃣ Empty State Tests

### Test 15: Empty Students Table
**Steps:**
1. Delete all sample students (if comfortable, or test on local copy)
2. View Students Management page

**Expected Result:**
- ✅ Shows empty state with:
  - Graduation cap icon
  - "No Data Found"
  - "No students found. Click 'Add Student' to get started."

---

### Test 16: Empty Teachers Table
**Steps:**
1. Delete all teachers
2. View Teachers Management page

**Expected Result:**
- ✅ Shows empty state with:
  - Chalkboard teacher icon
  - "No teachers found. Click 'Add Teacher' to get started."

---

### Test 17: Empty Filter Results
**Steps:**
1. Go to Students Management
2. Use filter: Class = `12-commerce` (if no students in this class)

**Expected Result:**
- ✅ Shows empty state message in table

---

## 6️⃣ Mobile Responsiveness Tests

### Test 18: Mobile Form Validation
**Steps:**
1. Open app on mobile device (or use Chrome DevTools mobile view)
2. Try adding student with invalid data
3. Check if error messages are readable

**Expected Result:**
- ✅ Error messages visible below fields
- ✅ Red text readable
- ✅ Form doesn't zoom on input focus (font-size: 16px prevents zoom)

---

### Test 19: Mobile Loading Spinner
**Steps:**
1. On mobile, save a student
2. Observe loading overlay

**Expected Result:**
- ✅ Spinner centered on screen
- ✅ Background dimmed
- ✅ Can't interact with form while loading

---

## 7️⃣ Edge Case Tests

### Test 20: WhatsApp Validation (Optional Field)
**Steps:**
1. Add student
2. Leave WhatsApp field empty → Should be OK ✅
3. Enter invalid WhatsApp: `12345` → Should show error ❌
4. Enter valid WhatsApp: `9123456789` → Should be OK ✅

---

### Test 21: Case-Insensitive Duplicate Username
**Steps:**
1. Add student with username: `TestUser`
2. Try to add another with username: `testuser` (lowercase)

**Expected Result:**
- ❌ Should detect as duplicate (case-insensitive check)

---

### Test 22: Case-Insensitive Duplicate Marks
**Steps:**
1. Add marks for test: `Unit Test 1`
2. Try to add marks for test: `unit test 1` (lowercase)

**Expected Result:**
- ❌ Should detect as duplicate (case-insensitive check)

---

### Test 23: Salary Negative Value Prevention
**Steps:**
1. Add teacher
2. Try to enter Salary: `-5000`

**Expected Result:**
- ✅ Input field has `min="0"` attribute (browser prevents negative)

---

## 🎯 Quick Test Checklist

Use this for quick regression testing:

- [ ] Add valid student → Success
- [ ] Add student with invalid phone → Error shown
- [ ] Add student with weak password → Error shown
- [ ] Add duplicate username → Error shown
- [ ] Fee paid > fee amount → Auto-corrected
- [ ] Fee status auto-calculates → Works
- [ ] Add valid teacher → Success
- [ ] Mark attendance → Success
- [ ] Mark duplicate attendance → Error shown
- [ ] Add marks → Success
- [ ] Add duplicate marks → Error shown
- [ ] Empty table shows empty state → Works
- [ ] Loading spinner appears during save → Works
- [ ] Mobile validation readable → Works

---

## 🐛 Bug Reporting

If you find any issues during testing, please note:

1. **Steps to reproduce**
2. **Expected behavior**
3. **Actual behavior**
4. **Browser & version** (Chrome, Firefox, Safari, etc.)
5. **Device** (Desktop, Mobile, Tablet)
6. **Screenshot** (if UI issue)

---

## ✅ Test Results Summary

After testing, fill this in:

| Test Category | Pass/Fail | Notes |
|---------------|-----------|-------|
| Student Validation | ⬜ | |
| Teacher Validation | ⬜ | |
| Attendance Validation | ⬜ | |
| Marks Validation | ⬜ | |
| Empty States | ⬜ | |
| Loading Indicators | ⬜ | |
| Mobile Responsive | ⬜ | |
| Edge Cases | ⬜ | |

---

**Tested By:** ___________________  
**Date:** ___________________  
**Overall Status:** ⬜ Pass / ⬜ Fail  
**Comments:** ___________________

---

## 🚀 All Tests Passed?

If all tests pass, the app is ready for production use! 🎉

Enjoy the improved ज्ञानसिंधू क्लासेस management system!
