# clone
trying to clone mintra in css

<?php
// Sample contribution data (dates with contributions)
$contributions = [
    '2024-03-03' => 1,
    '2024-03-04' => 1,
    '2024-03-10' => 1,
    '2024-03-11' => 1,
    '2024-03-17' => 1,
    '2024-03-18' => 1,
    '2024-03-24' => 1,
    '2024-03-25' => 1,
    '2024-03-31' => 1,
    '2024-04-01' => 1,
    '2024-04-28' => 1,
    '2024-05-05' => 1,
    '2024-05-06' => 5,
    '2024-05-11' => 1,
    '2024-05-12' => 1,
    '2024-05-27' => 3,
    '2025-01-04' => 1,
];
?>

<?php
function generateCalendar($year, $month, $contributions) {
    // Get the first day of the month and the number of days in the month
    $firstDay = new DateTime("$year-$month-01");
    $daysInMonth = $firstDay->format('t');
    
    // Get the first day of the week (0 = Sunday, 6 = Saturday)
    $startDay = $firstDay->format('w');
    
    // Start the calendar table
    $calendar = '<table class="contribution-calendar">';
    $calendar .= '<thead><tr><th colspan="7">' . $firstDay->format('F Y') . '</th></tr>';
    $calendar .= '<tr><th>Sun</th><th>Mon</th><th>Tue</th><th>Wed</th><th>Thu</th><th>Fri</th><th>Sat</th></tr></thead>';
    $calendar .= '<tbody><tr>';
    
    // Fill in the empty cells before the first day of the month
    for ($i = 0; $i < $startDay; $i++) {
        $calendar .= '<td></td>';
    }
    
    // Fill in the days of the month
    for ($day = 1; $day <= $daysInMonth; $day++) {
        $date = "$year-$month-" . str_pad($day, 2, '0', STR_PAD_LEFT);
        $contributionCount = isset($contributions[$date]) ? $contributions[$date] : 0;
        
        // Determine the class based on contribution count
        $class = 'level-' . min($contributionCount, 4); // Limit to level 4 for high contributions
        
        $calendar .= "<td class='$class' title='$contributionCount contributions on $date'>$day</td>";
        
        // Start a new row after Saturday
        if (($day + $startDay) % 7 == 0) {
            $calendar .= '</tr><tr>';
        }
    }
    
    // Fill in the empty cells after the last day of the month
    while (($day + $startDay) % 7 != 0) {
        $calendar .= '<td></td>';
        $day++;
    }
    
    $calendar .= '</tr></tbody></table>';
    return $calendar;
}

// Generate the calendar for March 2024
echo generateCalendar(2024, 3, $contributions);
?>

<style>
    .contribution-calendar {
        border-collapse: collapse;
        width: 100%;
        margin: 20px 0;
    }
    .contribution-calendar th, .contribution-calendar td {
        border: 1px solid #ddd;
        width: 14.28%; /* 100% / 7 days */
        height: 40px;
        text-align: center;
    }
    .level-0 {
        background-color: #f0f0f0; /* No contributions */
    }
    .level-1 {
        background-color: #c6e48b; /* Low contributions */
    }
    .level-2 {
        background-color: #7bc96f; /* Medium-low contributions */
    }
    .level-3 {
        background-color: #239a3b; /* Medium-high contributions */
    }
    .level-4 {
        background-color: #196127; /* High contributions */
    }
</style>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Contribution Calendar</title>
    <style>
        .contribution-calendar {
            border-collapse: collapse;
            width: 100%;
            margin: 20px 0;
        }
        .contribution-calendar th, .contribution-calendar td {
            border: 1px solid #ddd;
            width: 14.28%; /* 100% / 7 days */
            height: 40px;
            text-align: center;
        }
        .level-0 {
            background-color: #f0f0f0; /* No contributions */
        }
        .level-1 {
            background-color: #c6e48b; /* Low contributions */
        }
        .level-2 {
            background-color: #7bc96f; /* Medium-low contributions */
        }
        .level-3 {
            background-color: #239a3b; /* Medium-high contributions */
        }
        .level-4 {
            background-color: #196127; /* High contributions */
        }
    </style>
</head>
<body>

<?php
// Sample contribution data (dates with contributions)
$contributions = [
    '2024-03-03' => 1,
    '2024-03-04' => 1,
    '2024-03-10' => 1,
    '2024-03-11' => 1,
    '2024-03-17' => 1,
    '2024-03-18' => 1,
    '2024-03-24' => 1,
    '2024-03-25' => 1,
    '2024-03-31' => 1,
    '2024-04-01' => 1,
    '2024-04-28' => 1,
    '2024-05-05' => 1,
    '2024-05-06' => 5,
    '2024-05-11' => 1,
    '2024-05-12' => 1,
    '2024-05-27' => 3,
    '2025-01-04' => 1,
];

function generateCalendar($year, $month, $contributions) {
    $firstDay = new DateTime("$year-$month-01");
    $daysInMonth = $firstDay->format('t');
    $startDay = $firstDay->format('w');
    
    $calendar = '<table class="contribution-calendar">';
    $calendar .= '<thead><tr><th colspan="7">' . $firstDay->format('F Y') . '</th></tr>';
    $calendar .= '<tr><th>Sun</th><th>Mon</th><th>Tue</th><th>Wed</th><th>Thu</th><th>Fri</th><th>Sat</th></tr></thead>';
    $calendar .= '<tbody><tr>';
    
    for ($i = 0; $i < $startDay; $i++) {
        $calendar .= '<td></td>';
    }
    
    for ($day = 1; $day <= $daysInMonth; $day++) {
        $date = "$year-$month-" . str_pad($day, 2, '0', STR_PAD_LEFT);
        $contributionCount = isset($contributions[$date]) ? $contributions[$date] : 0;
        $class = 'level-' . min($contributionCount, 4);
        
        $calendar .= "<td class='$class' title='$contributionCount contributions on $date'>$day</td>";
        
        if (($day + $startDay) % 7 == 0) {
            $calendar .= '</tr><tr>';
        }
    }
    
    while (($day + $startDay) % 7 != 0) {
        $calendar .= '<td></td>';
        $day++;
    }
    
    $calendar .= '</tr></tbody></table>';
    return $calendar;
}

echo generateCalendar(2024, 3, $contributions);
?>

</body>
</html>
