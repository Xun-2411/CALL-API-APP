# Smart Note App - Quick Start Guide

## ⚡ Quick Setup & Run

### 1. Install Dependencies
```bash
flutter pub get
```

### 2. Run the App
```bash
flutter run
```

## 🎨 Customize Before Running

Edit `lib/main.dart` line that contains:
```dart
title: const Text('Smart Note - Nguyễn Văn A - SV000123'),
```

Replace `Nguyễn Văn A` with your **FULL NAME**  
Replace `SV000123` with your **STUDENT ID**

Example:
```dart
title: const Text('Smart Note - Trần Thị Liên - SV001029'),
```

## ✅ Feature Checklist

### HomeScreen (Main List)
- [x] AppBar showing: Smart Note - [Name] - [Student ID]
- [x] Search bar below AppBar (filters by title, real-time)
- [x] 2-column Staggered Grid layout
- [x] Note cards with: Title, Content preview, Timestamp
- [x] Empty state message
- [x] FAB (+) button to create notes

### DetailScreen (Edit/Create)
- [x] Minimalist white paper design
- [x] Title input field
- [x] Content multiline input (auto-expands)
- [x] Auto-save on back navigation
- [x] NO manual save button

### Delete Operations
- [x] Swipe from right to left to delete
- [x] Red background with trash icon appears
- [x] Confirmation dialog required
- [x] Only deletes after confirmation

### Data Persistence
- [x] Uses SharedPreferences
- [x] JSON serialization/deserialization
- [x] Survives app restart
- [x] Survives device restart

## 🧪 Quick Test Workflow

**Test 1: Create & Save**
1. Tap FAB (+)
2. Enter title: "Test Note 1"
3. Enter content: "This is a test"
4. (Optional) Tap "Đính kèm ảnh" and choose an image from gallery
5. Press back arrow
6. Should appear in list with correct timestamp and thumbnail if an image was added

**Test 2: Search**
1. Create another note: "My Shopping List"
2. Type "shopping" in search bar
3. Should filter to show only "My Shopping List"
4. Clear search - all notes return

**Test 3: Edit**
1. Tap any note
2. Edit the content
3. Press back
4. Return to list - changes saved
5. Timestamp should be updated

**Test 4: Delete**
1. Swipe a note from right to left
2. Red delete icon appears
3. Tap "Xóa" (Delete)
4. Note disappears from list

**Test 5: Persistence (IMPORTANT)**
1. Create 2-3 notes with different content
2. Kill the app (close it completely)
3. Reopen the app
4. All notes should still be there with same content

## 📝 Key Implementation Details

### Auto-Save Mechanism
```dart
// In DetailScreen
WillPopScope(
  onWillPop: () async {
    if (_hasChanges) {
      await _saveNote();  // Auto-save before leaving
    }
    Navigator.pop(context);
    return false;
  }
  ...
)
```

### Real-Time Search
```dart
void _filterNotes() {
  setState(() {
    _filteredNotes = _allNotes
        .where((note) => note.title.toLowerCase()
            .contains(_searchController.text.toLowerCase()))
        .toList();
  });
}
```

### JSON Persistence
```dart
// Saves notes as JSON array to SharedPreferences
Note.toJson() → jsonEncode() → SharedPreferences
SharedPreferences → jsonDecode() → Note.fromJson()
```

## 🎯 Expected Behavior

| Action | Expected Result |
|--------|-----------------|
| App Launch | Loads all saved notes from storage |
| Empty List | Shows "Bạn chưa có ghi chú nào..." |
| Tap FAB | Opens blank DetailScreen |
| Enter text & back | Auto-saves, returns to list with new note |
| Type in search | List filters in real-time by title |
| Tap note | Opens DetailScreen with existing note data |
| Swipe note | Red background appears with delete icon |
| Confirm delete | Note removed from list & storage |
| App restart | All notes reappear unchanged |

## 🐛 Troubleshooting

### Issue: Dependencies not found
```
Solution: Run `flutter pub get`
```

### Issue: Notes not saving
```
Solution: Ensure app is closed before restarting
         (not just backgrounded)
```

### Issue: Search not working
```
Solution: Type in the search bar below the AppBar
         It filters by note TITLE only
```

### Issue: Delete doesn't show confirmation
```
Solution: Wait for dialog to appear
         Confirm by tapping "Xóa" button
```

## 📊 Data Structure

Each note contains:
```json
{
  "id": "unique_timestamp",
  "title": "Note title",
  "content": "Note content can have\nmultiple lines",
  "createdAt": "2026-03-02T10:30:00.000Z",
  "updatedAt": "2026-03-02T10:35:00.000Z"
}
```

## 🔐 Offline Capability

✅ This app works 100% OFFLINE
- No internet connection required
- No API calls
- All data stored locally on device
- Works on airplane mode

## 📱 Platform Support

- ✅ Android
- ✅ iOS  
- ✅ Web
- ✅ Windows
- ✅ macOS
- ✅ Linux

---

**Ready to run!** Use `flutter run` to start the app.
