Here is a comprehensive, numbered testing checklist based on the specific architecture of the `Claude_Countdown_v8` scoreboard.

You can use this to track your validation progress. Each item is designed to test a specific logic branch or synchronization rule found in your code.

### 1. Connection & Room Initialization

1. [ ] **Room ID Generation**: Open the app and verify a unique 8-character alphanumeric hash appears in the URL.
2. [ ] **Room Consistency**: Refresh the browser and verify the Room ID in the URL remains identical.
3. [ ] **Cross-Device Pairing**: Scan the QR code or copy the URL to a second device; verify both show "Connected" (Green dot).
4. [ ] **Offline State**: Disable Wi-Fi/Data and verify the indicator turns Red with "Offline — reconnecting..." text.
5. [ ] **Server Offset**: Change the system clock on one device and verify the timer still synchronizes correctly (using the `serverTimeOffset` logic).

### 2. Team & Player Management

6. [ ] **Dynamic Team Addition**: Click "+ Add Team" and verify a new card appears on all connected devices within 1 second.
7. [ ] **Team Color Loop**: Add 8 teams and verify the color strip cycle restarts (Team 8 should have the same color as Team 1).
8. [ ] **Real-time Renaming**: Change a team name on Device A and verify the text updates on Device B without Device B losing focus if they were typing elsewhere.
9. [ ] **Input Sanitization**: Enter HTML tags (e.g., `<b>Test</b>`) as a team name and verify they are escaped and displayed as plain text.
10. [ ] **Team Deletion**: Remove a team and verify the "Total Points" and "Leading" stats update immediately for all users.
11. [ ] **Minimum Team Enforcement**: Attempt to delete teams until only one remains; verify the "Remove" button is disabled or non-functional.

### 3. Scoring & Atomic Transactions

12. [ ] **Score Increment**: Tap "+" and verify the score "pops" visually and increments on all screens.
13. [ ] **Atomic Concurrency**: Have two people spam the "+" button on the same team simultaneously. Verify the final score equals the total number of taps (no lost updates).
14. [ ] **Floor Limit**: Attempt to decrement a score of 0 and verify the score remains at 0 (no negative values).
15. [ ] **Custom Steps**: Change a team's step to ±5 or ±10; verify that tapping "+" adds that specific value for that team only.
16. [ ] **Step Sync**: Change the step value on Device A and verify the corresponding button on Device B highlights to match.

### 4. Timer Logic

17. [ ] **Global Sync**: Start the timer on one device; verify the countdown begins on all other devices simultaneously.
18. [ ] **Pause/Resume**: Pause the timer and verify the exact "Time Remaining" is frozen and displayed identically across all screens.
19. [ ] **Preset Switching**: Click a different time preset (e.g., 5 min) while the timer is running; verify it resets to the new time globally.
20. [ ] **Custom Input**: Enter "12" in the custom "mm" field and verify the timer sets to 12:00.
21. [ ] **Visual Warnings**: Verify the timer turns Orange at 10 seconds and Red/Blinking at 3 seconds.
22. [ ] **Audio/Visual Overlay**: Verify the "3, 2, 1" countdown overlay and the "🏁" icon appear at the correct intervals with accompanying beeps/alarms.

### 5. Leaderboard & Stats

23. [ ] **Leader Highlight**: Give one team a higher score than all others; verify the "Leading" crown and gold border appear only on that card.
24. [ ] **Tie Handling**: Create a tie for first place; verify the "Leading" crown disappears (as no single team is currently winning).
25. [ ] **Live Ranking**: Increase a lower team's score until it passes the leader; verify the "Leading" stat in the footer updates to the new team name.
26. [ ] **Stat Accuracy**: Verify "Total Points" and "Points Ahead" (Gap) calculations match the manual math of the visible scores.

### 6. Game History & Persistence

27. [ ] **Manual Save**: Click "Save Game" and verify a new entry appears in the "Game History" section with the current timestamp.
28. [ ] **Round Increment**: Click "Reset Scores"; verify all scores go to 0 and the Round Number increases by 1 globally.
29. [ ] **History Limit**: Save more than 60 games and verify the oldest entry is removed (pruning logic).
30. [ ] **Data Restoration**: Change current team names and scores, then click "Restore" on a history card. Verify the board reverts to the saved state.
31. [ ] **Local Cache**: Close all tabs, then reopen the Room URL; verify the "Last Saved" state loads from LocalStorage while waiting for Firebase.

### 7. UI/UX & Responsive Design

32. [ ] **Title Sync**: Change the "Score Board" title at the top and verify it updates for everyone after the 600ms debounce.
33. [ ] **Mobile Stacking**: View on a narrow phone and verify the Timer Panel and Action Bar wrap correctly without horizontal scrolling.
34. [ ] **QR Accuracy**: Open the QR modal and verify the URL displayed matches the URL in the browser's address bar.
35. [ ] **Toast Feedback**: Verify a green "Toast" message appears at the bottom center after actions like "Save" or "Reset".
