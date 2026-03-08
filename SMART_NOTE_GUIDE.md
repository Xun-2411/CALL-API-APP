# Smart Note Application - Guide & Customization

## ✅ Completed Features

### 1. **Model & Data Serialization**
- ✅ `Note` model with JSON serialization (toJson/fromJson)
- ✅ All notes include: title, content, timestamp (created & updated)
- ✅ Auto-generated unique IDs for each note

### 2. **Local Storage (SharedPreferences)**
- ✅ `StorageService` class for persistent data management
- ✅ Automatic JSON encoding/decoding
- ✅ Data persists even after closing the app
- ✅ Survives app restart and device restart

### 3. **Home Screen**
- ✅ AppBar with student information format
- ✅ Search bar with real-time filtering by note title
- ✅ 2-column Masonry/Staggered Grid layout
- ✅ Note cards showing: title, content preview (max 3 lines), timestamp
- ✅ Empty state message when no notes exist
- ✅ Floating Action Button (+) to create new notes

### 4. **Detail/Edit Screen**
- ✅ Minimalist white paper design
- ✅ Multiline text input for content
- ✅ Auto-save using WillPopScope hook
- ✅ No manual "Save" button - saves on back navigation
- ✅ Automatic timestamp update (updatedAt)
- ✅ Attachment gallery with image picker
- ✅ Remove attachments by tapping the "x" on thumbnails

### 5. **Attachments & Delete**
- ✅ Users can attach images to notes
- ✅ Detail screen includes "Đính kèm ảnh" button
- ✅ Attached images are stored as Base64 strings
- ✅ Thumbnail shows on note card if present
- ✅ Swipe-to-delete gesture from right to left
- ✅ Red background with trash icon on swipe
- ✅ Confirmation dialog before deletion
- ✅ Only deletes after user confirms

---

## 🎯 Customization Guide

### Edit AppBar Student Information
Open `lib/main.dart` and find the HomeScreen build method. Update this line:

```dart
title: const Text('Smart Note - Nguyễn Văn A - SV000123'),
```

Replace with your actual student name and ID:
```dart
title: const Text('Smart Note - [Your Name] - [Your Student ID]'),
```

### Change Color Scheme
In `AppBar` of `MyApp`:
```dart
theme: ThemeData(
  colorScheme: ColorScheme.fromSeed(seedColor: Colors.blue),  // Change Colors.blue
  useMaterial3: true,
),
```

Available options: `Colors.red`, `Colors.green`, `Colors.purple`, `Colors.orange`, etc.

### Customize Empty State Message
In `HomeScreen._buildEmptyState()`:
```dart
Text(
  'Your custom message here!',  // Edit this text
  style: TextStyle(...)
)
```

### Adjust Grid Layout
In `HomeScreen._buildNotesList()`:
```dart
MasonryGridView.count(
  crossAxisCount: 2,  // Change to 1 for single column
  mainAxisSpacing: 12,  // Adjust spacing
  crossAxisSpacing: 12,
  ...
)
```

### Change Note Card Appearance
Customize in `HomeScreen._buildNoteCard()`:
- Adjust `elevation` for shadow depth
- Change `BorderRadius.circular(12)` for corner radius
- Modify `padding` for internal spacing
- Adjust font sizes and colors

---

## 🚀 Testing Instructions

### 1. **Build & Run**
```bash
cd "c:\Flutter VS Code Project\flutter_application_1\flutter_application_2"
flutter run
```

### 2. **Create a New Note**
- Tap the FAB button (+)
- Enter a title (optional)
- Enter content
- Press back arrow or swipe back to auto-save

### 3. **Search Notes**
- Return to home screen
- Type in search bar to filter by title
- Search is case-insensitive and searches in real-time

### 4. **Edit a Note**
- Tap on any note card
- Edit title or content
- Navigate back to auto-save changes

### 5. **Delete a Note**
- On home screen, swipe a note card from right to left
- Red delete icon appears
- Tap OK in confirmation dialog to delete
- Or tap Cancel to keep the note

### 6. **Persistence Test (Critical)**
```
This is the required test to verify OFFLINE persistence:

Step A: Create 3-5 test notes
Step B: Close the app completely (kill from task manager)
Step C: Restart the app
Step D: Verify all notes are still there with correct content

Expected Result: All data should be intact
```

### 7. **Empty State**
- Delete all notes one by one
- Verify the empty state message appears
- Create a new note
- Empty state disappears

### 8. **Timestamp Verification**
- Create a note and check the timestamp
- Edit it after 1 minute
- The timestamp should update to reflect the edit time
- Creation time should remain unchanged

---

## 📱 File Structure

```
lib/
├── main.dart          # Complete app code
├── Note              # Model class (in main.dart)
├── StorageService    # Local storage service (in main.dart)
└── Screens:
    ├── HomeScreen    # Main list view
    └── DetailScreen  # Note editing view
```

---

## 🔧 Technical Details

### Dependencies
```yaml
shared_preferences: ^2.2.2     # Local data persistence
flutter_staggered_grid_view: ^0.7.0  # Masonry layout
```

### Key Classes & Methods

**Note Model**
- `Note()` - Constructor
- `toJson()` - Convert to JSON string
- `fromJson()` - Create from JSON object

**StorageService**
- `init()` - Initialize SharedPreferences
- `getNotes()` - Fetch all notes
- `saveNote()` - Create or update a note
- `deleteNote()` - Remove a note

**HomeScreen**
- `_filterNotes()` - Real-time search filtering
- `_buildNotesList()` - Render grid layout
- `_buildNoteCard()` - Individual note card with swipe-to-delete
- `_refreshNotes()` - Reload data after changes

**DetailScreen**
- Auto-save using `WillPopScope`
- Multiline text editing
- Automatic timestamp updating

---

## ✨ Best Practices Implemented

1. ✅ **Separation of Concerns** - StorageService handles all data operations
2. ✅ **JSON Serialization** - Proper encoding/decoding for persistence
3. ✅ **State Management** - Correct use of setState and FutureBuilder
4. ✅ **Error Handling** - Safe navigation and null checks
5. ✅ **UI/UX** - Responsive, accessible, and user-friendly
6. ✅ **Performance** - Efficient list rendering with staggered grid
7. ✅ **Offline First** - All operations work without internet

---

## 🎓 Learning Outcomes

After building this app, you should understand:

- ✅ Model classes and JSON serialization in Flutter
- ✅ How to use SharedPreferences for persistent storage
- ✅ Navigation between screens
- ✅ State management with setState
- ✅ Working with FutureBuilder for async operations
- ✅ Custom UI layouts (Masonry Grid, Dismissible)
- ✅ Text filtering and search functionality
- ✅ Confirmation dialogs and user interactions
- ✅ Proper lifecycle management with WillPopScope

---

## 💾 Storage Format

Notes are stored in SharedPreferences as JSON array:
```json
[
  {
    "id": "1234567890",
    "title": "My Note",
    "content": "Note content...",
    "createdAt": "2026-03-02T10:30:00.000Z",
    "updatedAt": "2026-03-02T10:35:00.000Z"
  }
]
```

---

**Version**: 1.0.0  
**Created**: March 2, 2026
