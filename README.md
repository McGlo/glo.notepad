﻿<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>...</title>
    <link rel="icon" href="favicon.ico" type="image/x-icon">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">
    <style>
        /* CSS Reset */
        html, body, h1, h2, h3, h4, h5, h6, p, ul, li {
            margin: 0;
            padding: 0;
        }

        /* Basic styling */
        body {
            font-family: 'Roboto', sans-serif; /* Use a modern and clean font */
            margin: 0;
    background-color: #f2f2f2; /* Light background color */
    color: #333; /* Dark text color */
            padding: 0;
        }

        /* Left-side bar styling */
        .sidebar {
            width: 270px;
            height: 102vh;
    background-color: #222; /* Dark background color */
    color: #fff; /* Light text color */
            float: left;
            padding: 0px;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;
            gap: 10px;
            overflow-y: auto;
            transition: width 0.3s ease-in-out;
        }

        .sidebar.collapsed {
            width: 0;
            overflow: hidden;
        }

        /* Note list styling */
        .note-list {
            list-style: none;
            padding: 0;
            margin: 0;
            margin-bottom: 10px;
            overflow-y: auto;
	    position: relative; /* Add position relative */
        }

        /* Note item styling */
        .note-item {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            margin-bottom: 10px;
            cursor: pointer;
            font-size: 14px;
            color: #fff;
    background-color: #444; /* Darker background color */
            padding: 10px;
            border-radius: 4px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
            transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
            width: calc(100% - 40px);
        }

        .note-item:hover {
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.6);
            transform: translateY(-1px);
    background-color: #333; /* Darker on hover and active */
        }

        .note-item:active {
            box-shadow: 0 1px 2px rgba(0, 0, 0, 0.8);
            transform: translateY(1px);
    background-color: #333; /* Darker on hover and active */
        }

        .note-item.selected {
            font-weight: bold;
    background-color: #222; /* Selected item color */
        }

        .note-item .icon {
            margin-right: 10px;
            cursor: pointer;
        }

        /* Title styling */
        .title {
            text-align: center;
            font-size: 24px;
            font-weight: bold;
            margin: 0px 0;
            color: #fff;
            padding: 5px 0;
        }

        /* Button styling */
        .sidebar button {
            display: block;
            padding: 5px 10px;
    background: #333; /* Blue accent color */
            color: #fff;
            border: none;
            cursor: pointer;
            width: 100%;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
            transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
            text-align: left;
        }

        .sidebar button:hover {
    background: #0056b3; /* Darker blue on hover */
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.6);
            transform: translateY(-1px);
        }

        .sidebar button:active {
            background: linear-gradient(to bottom, #000, #111);
            box-shadow: 0 1px 2px rgba(0, 0, 0, 0.8);
            transform: translateY(1px);
        }

  body, html {
    height: 100%;
    margin: 0;
    font-size: 13px; /* Default font size */
  }

        /* Notepad container styling */
        .notepad-container {
            padding: 20px;
            box-sizing: border-box;
            height: 100%;
            display: flex;
            align-items: flex-start;
            justify-content: flex-start;
            transition: padding-left 0.3s ease-in-out, justify-content 0.3s ease-in-out;
    flex-direction: column; /* Stack items vertically */
        }

  #text-area, #additional-text-area {
    height: 100%;
    font-size: 13px; /* Default font size */
    box-sizing: border-box;
    border: 1px solid #ddd; /* Optional: Add border for better visibility */
    padding: 10px; /* Optional: Add padding for better appearance */
    margin: 0;
    resize: none;
  }

  .text-area-container {
    flex: 1;
    width: 70%;
    padding-right: 10px; /* Add padding between main and additional text areas */
  }

        .notepad-container.collapsed {
            padding-left: 20px;
            justify-content: center;
            padding-left: 0px;  /* Remove left padding when sidebar is collapsed */
            padding-right: 300px; /* Remove right padding when sidebar is collapsed */
            flex: 2;
        }

.notepad-container.collapsed .sidebar {
    display: none; /* Hide the sidebar when collapsed */
}


  .additional-text-area-container {
    flex: 1;
    width: 30%;
    padding-left: 10px; /* Add padding between main and additional text areas */
  }

        /* Text area styling */
.text-area {
    width: 100%;
    height: 100%;
    border: 1px solid #ddd;
    padding: 15px;
    font-size: 16px;
    line-height: 1.6;
    outline: none;
    resize: vertical;
    overflow: auto;
    color: #333;
    transition: width 0.3s ease-in-out;
    font-family: 'Arial', sans-serif; /* Use a classic and professional font */
    background-color: #fff; /* White background */
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    box-sizing: border-box; /* Include padding and border in the element's total width and height */
}

/* Apply this rule when the sidebar is collapsed */
.sidebar.collapsed .text-area {
    width: calc(100% - 270px); /* Adjust the width when the sidebar is collapsed */
}

/* Optional: Add a slight border highlight when focused */
.text-area:focus {
    border-color: #333; /* Highlight border on focus */
}

        /* Floating sidebar toggle icon */
        .toggle-icon {
            position: fixed;
            top: 50%;
            left: 0;
            transform: translateY(-50%);
            background-color: #333;
            color: #fff;
            padding: 12px;
            border-radius: 5%;
            cursor: pointer;
            transition: background-color 0.3s ease-in-out, color 0.3s ease-in-out, transform 0.3s ease-in-out;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
        }

        .toggle-icon:hover {
            background-color: #555; /* Darker blue on hover */
            color: #fff;
        }

        .toggle-icon:active {
            background-color: #003366; /* Dark blue on active */
        }

        .notepad-container.collapsed .toggle-icon {
            transform: translateY(-50%) rotate(180deg); /* Rotate icon when sidebar is collapsed */
        }

        /* Add a slight shadow effect to the icon */
        .toggle-icon::before {
            content: "";
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 32px;
            height: 32px;
            background: radial-gradient(circle, #0000 0%, #0003 60%, #0008 100%);
            border-radius: 5%;
            opacity: 0;
            transition: opacity 0.3s ease-in-out;
        }

        .toggle-icon:hover::before {
            opacity: 1;
        }

        /* Browser extension container */
        .extension-container {
            position: absolute;
            bottom: 10px;
            right: 10px;
            padding: 5px;
            border: 1px solid #ccc;
            border-radius: 4px;
            background-color: #fff;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }

        /* Note timestamps */
        .note-timestamp {
            font-size: 12px;
            color: #ccc;
            margin-top: 5px;
        }

        /* Search bar styling */
        #searchBar {
            width: 100%;
            padding: 10px;
            border: none;
            border-bottom: 20px solid #333;
            font-size: 16px;
            outline: none;
            background-color: #f5f5f5;
            transition: border-color 0.3s ease-in-out;
            position: sticky;
            top: 0;
            z-index: 1;
        }

        #searchBar:focus {
            background-color: #fff;
        }

        /* Text editor styling */
        .text-editor {
            margin-bottom: 10px;
        }

        .button-container {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 5px;
            justify-items: center;
        }

        .text-editor .icon {
            padding: 10px;
            font-weight: bold;
            border: none;
            cursor: pointer;
            background-color: #444;
            color: #fff;
            transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
            border-radius: 4px;
            text-align: center;
        }

        .text-editor .icon:hover {
            background-color: #007bff; /* Change to a contrasting color on hover */
            transform: translateY(-2px);
        }

        .text-editor .icon:last-child {
            margin-right: 0;
        }

        /* Highlight the selected button */
        .text-editor .icon.active {
            background-color: #007bff;
            transform: translateY(-2px);
        }

        .line-separator {
            width: 100%;
            height: 1px;
            background-color: #ccc;
            margin: 10px 0;
        }

        .resizable-image {
            max-width: 100%;
            max-height: 100%;
            width: auto;
            height: auto;
        }

        .text-editor .icon.modify-pixel {
            padding: 10px;
            font-weight: bold;
            border: none;
            cursor: pointer;
            background-color: #333;
            color: #fff;
            transition: background-color 0.3s ease-in-out;
            border-radius: 4px;
        }

        .text-editor .icon.modify-pixel:hover {
            background-color: #444;
        }

        .resizable-image.selectable-image {
            cursor: pointer;
            max-width: 100%;
            max-height: 100%;
            width: auto;
            height: auto;
            border: 2px solid transparent;
            transition: border-color 0.3s ease-in-out;
        }

        .resizable-image.selectable-image:hover {
            border-color: #007bff;
        }

        .resizable-image.selected {
            border: 2px solid #007bff;
        }

        /* Popup container */
.popup {
    max-height: 80vh;
    overflow-y: auto;
    display: none;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: linear-gradient(45deg, #e0e0e0 0%, #ffffff 100%); /* Adjust the gradient */
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
    z-index: 1000;
    width: 70%;
    max-width: 600px;
    font-family: Arial, sans-serif;
    border: 2px solid #ccc;
}


        .popup p {
            font-size: 16px;
            line-height: 1.5;
            color: #333;
            margin-bottom: 10px;
        }

        .popup a {
            color: #007bff;
            text-decoration: underline;
        }

        .popup a:hover {
            color: #0056b3;
        }

.close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    width: 40px; /* Increased button size */
    height: 40px; /* Increased button size */
    background-color: #fff; /* Set background color to match pop-up background */
    border: none;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 50%; /* Make it a circular button */
    transition: background-color 0.3s ease-in-out;
}

.close-button:hover {
    background-color: #ddd; /* Change background color on hover if needed */
}

.close-button::before {
    content: "\2715"; /* Unicode for X icon */
    color: #333; /* Set color to match text color */
    font-size: 24px; /* Increased icon size for HD appearance */
    line-height: 40px; /* Center the icon vertically */
    font-weight: bold; /* Set font weight to bold */
}




.close-button::before {
    transform: translate(-50%, -50%) rotate(-45deg);
}


.close-button::before {
    content: "\2715"; /* Unicode for X icon */
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 20px;
    height: 20px;
    line-height: 20px; /* Centering the X vertically */
    font-size: 18px; /* Adjust the size of the X icon */
    color: #333; /* Set color to a professional-looking dark color */
}

.close-button::after {
    content: none; /* Remove the content of the ::after pseudo-element */
}


        .popup h2 {
            font-size: 24px;
            margin-bottom: 15px;
            color: #007BFF; /* Blue title color */
            font-family: Arial, sans-serif;
            background-color: #f9f9f9;
            border: 2px solid #ddd;
            border-radius: 5px;
            padding: 20px;
        }

        .business-title {
            background-color: #007bff;
            color: #fff;
            padding: 10px;
            border-radius: 5px 5px 0 0;
        }

        .result, .next-business {
            margin-top: 15px;
            padding: 20px;
            border: 2px solid #007bff;
            border-radius: 5px;
            background-color: #f9f9f9;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

.popup::before {
    content: "";
    position: absolute;
    top: -10px;
    left: -10px;
    right: -10px;
    bottom: -10px;
    background-image: linear-gradient(45deg, #e0e0e0 0%, #ffffff 100%);
    border-radius: 12px;
    z-index: -1;
}

        @media screen and (max-width: 600px) {
            .popup {
                width: 90%;
                max-width: none;
                padding: 15px;
            }
        }

<!-- Add this style block within the <style> tags of your document -->
<style>
  /* Style for the popup container */
.popup {
    display: none;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    padding: 20px;
    max-width: 600px;
    width: 100%;
    border-radius: 8px;
    z-index: 1000;
}

.popup section {
    margin-bottom: 20px;
}

.popup h2 {
    color: #333;
}

.popup table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
}

.popup th, .popup td {
    padding: 12px;
    border: 1px solid #ddd;
    text-align: left;
}

.popup th {
    background-color: #007BFF;
    color: #fff;
}

.popup tbody tr:hover {
    background-color: #f0f0f0;
}

.popup button {
    background-color: #007BFF;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
}

.popup button:hover {
    background-color: #0056b3;
}

.popup .close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    background-color: #ddd;
    padding: 8px 16px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.popup .close-button:hover {
    color: #333; /* Darken close button color on hover */
}

/* Optional Animation */
.note-item,
.sidebar button,
.toggle-icon,
.popup,
.popup button,
.popup .close-button {
    transition: background-color 0.3s ease-in-out, color 0.3s ease-in-out, transform 0.3s ease-in-out;
}

.note-item:hover,
.note-item:active,
.sidebar button:hover,
.toggle-icon:hover,
.popup button:hover,
.popup .close-button:hover {
    transform: translateY(-2px);
}

  /* Style for the table */
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
  }

  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }

  th {
    background-color: #f2f2f2;
  }

/* Placeholder input styles */
.popup input[type="text"] {
    width: 100%;
    padding: 10px;
    margin-top: 5px;
    margin-bottom: 15px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-sizing: border-box;
    font-size: 16px;
}

/* Result and next business day styles */
.popup p {
    margin-bottom: 10px;
    font-size: 16px;
}

.popup span {
    font-weight: bold;
    color: #007BFF; /* You can adjust the color as needed */
}

/* Business day input styles */
.popup input[type="text"] {
    width: calc(100% - 20px);
    padding: 10px;
    margin: 5px 0 15px 0;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-sizing: border-box;
    font-size: 16px;
}

.popup button {
    background-color: #007BFF;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
}

.popup button:hover {
    background-color: #0056b3;
}

.popup button,
.popup input[type="text"] {
    display: inline-block;
}

.popup h2 {
    color: #333;
    margin-bottom: 15px;
}

.popup section {
    margin-bottom: 20px;
}

/* Title styles for different business day sections */
.popup h2 {
    color: #000; /* Black color for titles */
    font-size: 24px;
    margin-bottom: 15px;
}

/* Title styles for the "Holiday Dates" section */
.popup h2.holiday-title {
    color: #000; /* Black color for holiday title */
}

/* Table styles for the "Holiday Dates" section */
.popup table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
}

.popup th, .popup td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
}

.popup th {
    background-color: #007BFF;
    color: #fff;
}

.popup tbody tr:nth-child(even) {
    background-color: #f2f2f2;
}

.popup tbody tr:hover {
    background-color: #ddd;
}

  .delete-confirmation {
    display: none;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    padding: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    text-align: center;
    animation: fadeIn 0.3s ease-in-out;
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  .delete-confirmation h3 {
    margin-bottom: 10px;
    color: #333;
  }

  .delete-confirmation button {
    background-color: #ff5a5f;
    color: #fff;
    border: none;
    padding: 8px 15px;
    margin: 0 10px;
    cursor: pointer;
    border-radius: 3px;
    transition: background-color 0.3s ease-in-out;
  }

  .delete-confirmation button:hover {
    background-color: #d9534f;
  }

  .delete-confirmation button.cancel {
    background-color: #5bc0de;
  }

  .delete-confirmation button.cancel:hover {
    background-color: #46b8da;
  }

  @keyframes fadeOut {
    from {
      opacity: 1;
    }
    to {
      opacity: 0;
    }
  }


  /* New styles for rename confirmation */
  .rename-confirmation {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 20px;
    background-color: #fff;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    text-align: center;
    animation: fadeIn 0.3s ease-in-out;
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  /* Styles for the input and buttons */
  .rename-input {
    width: 80%;
    padding: 8px;
    margin-bottom: 10px;
  }

  .rename-buttons {
    display: flex;
    justify-content: space-around;
  }

  .rename-button {
    padding: 8px 16px;
    background-color: #4CAF50;
    color: #fff;
    border: none;
    border-radius: 3px;
    cursor: pointer;
  }

  .rename-button.cancel {
    background-color: #ccc;
  }

.custom-prompt {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: #ffffff;
    padding: 20px;
    border: 2px solid #3498db;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    z-index: 1000;
    max-width: 400px;
    width: 100%;
    text-align: center;
}

.custom-prompt input {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    box-sizing: border-box;
}

.custom-prompt button {
    background-color: #3498db;
    color: #ffffff;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.custom-prompt button.cancel {
    background-color: #95a5a6;
    margin-left: 10px;
}


/* Default styles for the text areas */
#text-area,
#additional-text-area {
  box-sizing: border-box; /* Include padding and borders in the total width and height */
  width: 100%; /* Take up 100% width */
  padding: 10px; /* Add padding as needed */
}

/* Set the height of the text area to 70% and the additional text area to 30% */
#text-area {
    flex: 7; /* 70% of the height */
    width: 100%;
  }

.collapsed #text-area {
  width: calc(100% - 40px);
}

#additional-text-area {
    flex: 3; /* 30% of the height */
    width: 100%;
  }

/* Media query for smaller screens and when the sidebar is hidden */
@media screen and (max-width: 600px) {
  #text-area,
  #additional-text-area {
    height: auto; /* Reset height for smaller screens */
    padding: 5px; /* Adjust padding for smaller screens if needed */
  }
}

/* Media query for when the sidebar is hidden */
@media screen and (max-width: 1200px) {
  .collapsed #text-area,
  .collapsed #additional-text-area {
    height: 100%; /* Occupy full height when the sidebar is hidden */
  }
}

/* Media query for smaller screens */
@media screen and (max-width: 600px) {
  .collapsed #text-area {
    width: 100%; /* Occupy full width when collapsed on smaller screens */
  }
}

.transition {
  transition: width 0.3s ease-in-out; /* Adjust the duration and easing as needed */
}

        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        .notepad-container {
            display: flex;
            height: 100vh;
        }
        .text-area {
            flex: 1;
            padding: 20px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            outline: none;
            resize: none;
            font-size: 16px;
            background-color: #fff;
            overflow-y: auto;
        }
        .popup {
            width: 80%;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        #closeButton {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 16px;
        }


.calendar-popup {
    display: none;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    padding: 20px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
    border-radius: 10px;
    z-index: 1000;
    width: 90%;
    max-width: 600px;
    font-family: 'Arial', sans-serif;
}

.calendar-popup table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
}

.calendar-popup th, .calendar-popup td {
    padding: 10px;
    border: 1px solid #ddd;
    text-align: center;
    font-size: 14px;
}

.calendar-popup th {
    background-color: #007bff;
    color: #fff;
}

.calendar-popup .blue {
    background-color: #cce5ff;
}

.calendar-popup .red {
    background-color: #f8d7da;
}

.close-button-icon {
    position: absolute;
    top: 10px;
    right: 10px;
    background-color: transparent;
    color: #333;
    border: none;
    font-size: 24px;
    cursor: pointer;
    font-weight: bold;
}

.info-button {
    position: absolute;
    right: 10px;
    top: 5px;
    cursor: pointer;
    background-color: #007bff;
    color: #fff;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    font-size: 14px;
}

.calendar-container {
    margin-bottom: 20px;
}

    .holiday {
        background-color: red;
        cursor: pointer; /* Use pointer cursor */
    }

    .banner {
        background-color: #f0f0f0;
        border: 1px solid #ccc;
        padding: 10px;
        margin-top: 20px;
        border-radius: 5px;
    }

    .banner h3 {
        margin-bottom: 10px;
        font-family: 'Arial', sans-serif;
        font-size: 18px;
        font-weight: bold;
        color: #333;
    }

    .banner ul {
        list-style-type: none;
        padding: 0;
        font-family: 'Arial', sans-serif;
        font-size: 14px;
        color: #555;
    }

    .banner li {
        margin-bottom: 5px;
    }

    .calendar-container {
        font-family: 'Arial', sans-serif;
        font-size: 14px;
        color: #333;
    }

    .calendar-container h3 {
        font-size: 18px;
        font-weight: bold;
    }

    .calendar-container table {
        width: 100%;
        border-collapse: collapse;
    }

    .calendar-container th, .calendar-container td {
        padding: 8px;
        text-align: center;
        border: 1px solid #ccc;
    }

    </style>
    <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/date-fns/2.23.0/date_fns.min.js"></script>
</head>

<body>
    <div class="sidebar">

<div class="text-editor">
    <div class="button-container">

<!-- Assuming you have an icon with the id "insertHorizontalLineIcon" -->
<button class="icon" onclick="insertHorizontalLine()"><span>&#8213;</span></button>

        <!-- Add more buttons as needed -->
        <button class="icon" onclick="changeTextSize()">Size</button>
        <button class="icon" onclick="alignText('left')">Left</button>
        <button class="icon" onclick="alignText('center')">Center</button>
        <button class="icon" onclick="alignText('right')">Right</button>
	<button class="icon" onclick="attachImage()">📷</button>
<input type="file" id="imageInput" style="display: none;" accept="image/*" onchange="insertImage(event)">
    </div>
</div>

<div class="note-list">
    <input type="search" id="searchBar" placeholder="Search notes...">
    <ul></ul>
</div>
        <div>
            <button class="note-item" onclick="addNote()">Add Note</button>
            <button class="note-item" onclick="exportData()">Export</button>
<input type="file" id="importInput" accept=".json" style="display: none;" onchange="importData(event)">
<button class="note-item" onclick="triggerFileInput()">Import</button>
	    <button class="note-item" onclick="openBusinessDayCalculator()">Business Day Calculator</button>
<button id="maximizeButton" class="note-item">Maximize</button>



        </div>
    </div>

<div id="businessDayPopup" class="popup">
    <!-- Close button -->
    <button class="close-button" onclick="closeBusinessDayPopup()"></button>
    <section>
        <h2>2 Business Days | DNR/TTLTS</h2>
        <div style="position: relative;">
            <input type="text" id="business-days-2" placeholder="mm/dd/yyyy" onchange="calculateBusinessDay('business-days-2', 'result-2', 'next-business-day-2', 2)">
            <button class="info-button" id="info-button-2" style="display:none;" onclick="showCalendar('business-days-2', 2)">i</button>
        </div>
        <p>Result: <span id="result-2"></span></p>
        <p>Next Business Day: <span id="next-business-day-2"></span></p>
    </section>

    <section>
        <h2>5 Business Days | LAB</h2>
        <div style="position: relative;">
            <input type="text" id="business-days-5" placeholder="mm/dd/yyyy" onchange="calculateBusinessDay('business-days-5', 'result-5', 'next-business-day-5', 5)">
            <button class="info-button" id="info-button-5" style="display:none;" onclick="showCalendar('business-days-5', 5)">i</button>
        </div>
        <p>Result: <span id="result-5"></span></p>
        <p>Next Business Day: <span id="next-business-day-5"></span></p>
    </section>

    <section>
        <h2>9 Business Days | Late Shipment</h2>
        <div style="position: relative;">
            <input type="text" id="business-days-9" placeholder="mm/dd/yyyy" onchange="calculateBusinessDay('business-days-9', 'result-9', 'next-business-day-9', 9)">
            <button class="info-button" id="info-button-9" style="display:none;" onclick="showCalendar('business-days-9', 9)">i</button>
        </div>
        <p>Result: <span id="result-9"></span></p>
        <p>Next Business Day: <span id="next-business-day-9"></span></p>
    </section>

    <section>
        <h2>14 Business Days | Late Shipment</h2>
        <div style="position: relative;">
            <input type="text" id="business-days-14" placeholder="mm/dd/yyyy" onchange="calculateBusinessDay('business-days-14', 'result-14', 'next-business-day-14', 14)">
            <button class="info-button" id="info-button-14" style="display:none;" onclick="showCalendar('business-days-14', 14)">i</button>
        </div>
        <p>Result: <span id="result-14"></span></p>
        <p>Next Business Day: <span id="next-business-day-14"></span></p>
    </section>

    <section>
        <h2>20 Business Days | Return Timeframe</h2>
        <div style="position: relative;">
            <input type="text" id="business-days-20" placeholder="mm/dd/yyyy" onchange="calculateBusinessDay('business-days-20', 'result-20', 'next-business-day-20', 20)">
            <button class="info-button" id="info-button-20" style="display:none;" onclick="showCalendar('business-days-20', 20)">i</button>
        </div>
        <p>Result: <span id="result-20"></span></p>
        <p>Next Business Day: <span id="next-business-day-20"></span></p>
   

<div class="calendar-popup" id="calendar-popup">
    <button class="close-button-icon" onclick="closeCalendar()">✖</button>
    <h3 id="calendar-title">Calendar</h3>
    <table id="calendar-table">
        <thead>
            <tr>
                <th>Su</th>
                <th>Mo</th>
                <th>Tu</th>
                <th>We</th>
                <th>Th</th>
                <th>Fr</th>
                <th>Sa</th>
            </tr>
        </thead>
        <tbody id="calendar-body">
            <!-- Calendar dates will be dynamically populated here -->
        </tbody>
    </table>
 </section>

</div>
  </section>
  <div class="notepad-container">
    <div class="toggle-icon" onclick="toggleSidebar()">☰</div>
    <div id="text-area" class="text-area" contenteditable spellcheck="true"></div>
    <div id="additional-text-area" class="text-area" contenteditable spellcheck="true"></div>
    <div class="extension-container">
      <!-- Include your browser extension here -->
    </div>
  </div>

    <script>

document.querySelectorAll('input[type="text"]').forEach(input => {
    input.addEventListener('change', function(event) {
        const inputId = event.target.id;
        const infoButton = document.getElementById(`info-button-${inputId.split('-').pop()}`);
        if (event.target.value) {
            infoButton.style.display = 'inline';
            closeCalendar();
        } else {
            infoButton.style.display = 'none';
        }
    });
});

function showCalendar(inputId, businessDays) {
    const inputDate = document.getElementById(inputId).value;
    if (inputDate) {
        const startDate = new Date(inputDate);
        renderCalendarsForBusinessDays(startDate, businessDays);
    }
}

function renderCalendarsForBusinessDays(startDate, businessDays) {
    const calendarPopup = document.getElementById('calendar-popup');
    calendarPopup.innerHTML = ''; // Clear previous content

    const endDate = calculateEndDate(startDate, businessDays);

    const startYear = startDate.getFullYear();
    const endYear = endDate.getFullYear();

    if (startYear !== endYear) {
        // Render calendars for both years
        renderYearlyCalendar(startDate, endDate, businessDays, startYear);
        renderYearlyCalendar(startDate, endDate, businessDays, endYear);
    } else {
        // Render calendar for a single year
        renderYearlyCalendar(startDate, endDate, businessDays, startYear);
    }

    calendarPopup.style.display = 'block';
}

function renderYearlyCalendar(startDate, endDate, businessDays, year) {
    const startMonth = year === startDate.getFullYear() ? startDate.getMonth() : 0;
    const endMonth = year === endDate.getFullYear() ? endDate.getMonth() : 11;

    for (let month = startMonth; month <= endMonth; month++) {
        const calendarHtml = createCalendarHtml(startDate, endDate, businessDays, year, month);
        document.getElementById('calendar-popup').innerHTML += calendarHtml;
    }
}


function createCalendarHtml(startDate, endDate, businessDays, year, month) {
    const calendarTitle = `Calendar for ${new Date(year, month).toLocaleDateString('en-US', { month: 'long', year: 'numeric' })}`;
    let calendarHtml = `
        <div class="calendar-container">
            <h3>${calendarTitle}</h3>
            <button class="close-button-icon" onclick="closeCalendar()">✖</button>
            <table>
                <thead>
                    <tr>
                        <th>Su</th>
                        <th>Mo</th>
                        <th>Tu</th>
                        <th>We</th>
                        <th>Th</th>
                        <th>Fr</th>
                        <th>Sa</th>
                    </tr>
                </thead>
                <tbody>`;

    const daysInMonth = new Date(year, month + 1, 0).getDate();
    const startDay = new Date(year, month, 1).getDay();
    let currentDay = 1;
    let businessDaysCount = 0;
    let dateWithinTimeframe = new Date(startDate);
    dateWithinTimeframe.setDate(startDate.getDate() + 1);

    for (let i = 0; i < 6; i++) {
        calendarHtml += '<tr>';
        for (let j = 0; j < 7; j++) {
            if (i === 0 && j < startDay || currentDay > daysInMonth) {
                calendarHtml += '<td></td>';
            } else {
                const cellDate = new Date(year, month, currentDay);
                let className = '';

                if (isBusinessDay(cellDate) && cellDate > startDate && cellDate <= endDate) {
                    className = 'blue'; // Highlight business days within the timeframe
                    businessDaysCount++;
                } else if (isFederalHoliday(cellDate)) {
                    className = 'holiday'; // Highlight US federal holidays
                }

                calendarHtml += `<td class="${className}">${currentDay}</td>`;
                currentDay++;
            }
        }
        calendarHtml += '</tr>';
    }

    calendarHtml += '</tbody></table>';
    calendarHtml += displayHolidayList(year, month);
    calendarHtml += `</div>`;
    return calendarHtml;
}

function displayHolidayList(year, month) {
    const holidays = {
        '2024-01-01': "New Year's Day",
        '2024-01-15': "Martin Luther King, Jr. Day",
        '2024-02-19': "Washington's Birthday",
        '2024-05-27': "Memorial Day",
        '2024-06-19': "Juneteenth",
        '2024-07-04': "Independence Day",
        '2024-09-02': "Labor Day",
        '2024-10-14': "Columbus Day",
        '2024-11-11': "Veterans Day",
        '2024-11-28': "Thanksgiving Day",
        '2024-12-25': "Christmas Day",
        '2025-01-01': "New Year's Day",
        '2025-01-20': "Martin Luther King, Jr. Day",
        '2025-02-17': "Washington's Birthday",
        '2025-05-26': "Memorial Day",
        '2025-06-19': "Juneteenth",
        '2025-07-04': "Independence Day",
        '2025-09-01': "Labor Day",
        '2025-10-13': "Columbus Day",
        '2025-11-11': "Veterans Day",
        '2025-11-27': "Thanksgiving Day",
        '2025-12-25': "Christmas Day"
    };

    let holidayHtml = '<div class="banner">';
    holidayHtml += `<h3>Holidays in ${new Date(year, month).toLocaleDateString('en-US', { month: 'long', year: 'numeric' })}</h3>`;
    holidayHtml += '<ul>';

    const monthYearString = `${year}-${String(month + 1).padStart(2, '0')}`;

    for (const [date, holiday] of Object.entries(holidays)) {
        if (date.startsWith(monthYearString)) {
            holidayHtml += `<li>${date.split('-')[2]}: ${holiday}</li>`;
        }
    }

    holidayHtml += '</ul></div>';
    return holidayHtml;
}

// Function to get the holiday name based on the date
function getHolidayName(date) {
    const holidays = {
        '2024-01-01': "New Year's Day",
        '2024-01-15': "Martin Luther King, Jr. Day",
        '2024-02-19': "Washington's Birthday",
        '2024-05-27': "Memorial Day",
        '2024-06-19': "Juneteenth",
        '2024-07-04': "Independence Day",
        '2024-09-02': "Labor Day",
        '2024-10-14': "Columbus Day",
        '2024-11-11': "Veterans Day",
        '2024-11-28': "Thanksgiving Day",
        '2024-12-25': "Christmas Day",
        '2025-01-01': "New Year's Day",
        '2025-01-20': "Martin Luther King, Jr. Day",
        '2025-02-17': "Washington's Birthday",
        '2025-05-26': "Memorial Day",
        '2025-06-19': "Juneteenth",
        '2025-07-04': "Independence Day",
        '2025-09-01': "Labor Day",
        '2025-10-13': "Columbus Day",
        '2025-11-11': "Veterans Day",
        '2025-11-27': "Thanksgiving Day",
        '2025-12-25': "Christmas Day"
    };

    const dateString = date.toISOString().split('T')[0]; // Format the date as YYYY-MM-DD
    return holidays[dateString] || '';
}






function closeCalendar() {
    document.getElementById('calendar-popup').style.display = 'none';
}

// Function to calculate the end date considering business days
function calculateEndDate(startDate, businessDays) {
    let currentDate = new Date(startDate);
    let businessDaysCount = 0;

    while (businessDaysCount < businessDays) {
        currentDate.setDate(currentDate.getDate() + 1);
        if (isBusinessDay(currentDate)) {
            businessDaysCount++;
        }
    }

    return currentDate;
}









// Event listener to toggle sidebar visibility on Tab key press
document.addEventListener("keydown", function(event) {
    if (event.key === "Tab") {
        // Prevent default Tab key behavior (e.g., moving focus)
        event.preventDefault();
        // Toggle sidebar visibility
        toggleSidebar();
    }
});


// Function to calculate business days
function calculateBusinessDays(startDate, daysToAdd) {
    const millisecondsPerDay = 24 * 60 * 60 * 1000;
    const weekendDays = [0, 6]; // Sunday (0) and Saturday (6)
    let currentDate = new Date(startDate.getTime());

    // Loop through each day to add
    for (let i = 0; i < daysToAdd; i++) {
        currentDate.setDate(currentDate.getDate() + 1);
        // Check if the current day is a weekend day
        if (weekendDays.includes(currentDate.getDay())) {
            daysToAdd++;
        }
    }
    return currentDate;
}

// Function to calculate business days for "5 Business Days | LAB"
function calculate5BusinessDays(startDate) {
    return calculateBusinessDays(startDate, 5);
}

// Function to update the popup with the calculated date for "5 Business Days | LAB"
function update5BusinessDaysPopup() {
    const startDate = new Date();
    const businessDaysLabDate = calculate5BusinessDays(startDate);
    const formattedDate = businessDaysLabDate.toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
    const popupContent = `5 Business Days | LAB: ${formattedDate}`;
    document.getElementById('popupContent').innerText = popupContent;
}














let initialSelectedNoteId = null;

// Function to store the window size
function storeWindowSize(window) {
    const { outerWidth: width, outerHeight: height } = window;
    localStorage.setItem("popupWindowSize", JSON.stringify({ width, height }));
}

// Function to retrieve the stored window size
function getStoredWindowSize() {
    return JSON.parse(localStorage.getItem("popupWindowSize")) || { width: 600, height: 400 };
}

// Function to get the ID of the currently selected note
function getSelectedNoteId() {
    const selectedNote = document.querySelector(".note-item.selected");
    return selectedNote ? selectedNote.id : null;
}

// Function to update the note content
function updateNoteContent(noteId, mainContent, additionalContent) {
    if (noteId) {
        const note = document.getElementById(noteId);
        if (note) {
            note.querySelector(".note-content").innerHTML = mainContent;
            note.querySelector(".additional-note-content").innerHTML = additionalContent;
        }
    }
}

// Event listener for the maximize button
document.getElementById("maximizeButton").addEventListener("click", function() {
    initialSelectedNoteId = getSelectedNoteId();
    const savedWindowSize = getStoredWindowSize();
    const mainTextAreaContent = document.getElementById("text-area").innerHTML;
    const additionalTextAreaContent = document.getElementById("additional-text-area").innerHTML;

    const popupWindow = window.open("", "_blank", `width=${savedWindowSize.width},height=${savedWindowSize.height},resizable,scrollbars`);
    if (!popupWindow) {
        alert('Failed to open the popup window.');
        return;
    }
    const popupDocument = popupWindow.document;

    // Create and style elements
    const style = popupDocument.createElement("style");
    style.innerHTML = `
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            display: flex;
            flex-direction: column;
            align-items: stretch;
            height: 100vh;
            box-sizing: border-box;
        }
        .text-area {
            width: 100%;
            border: 1px solid #ddd;
            padding: 15px;
            font-size: 13px;
            line-height: 1.6;
            outline: none;
            resize: none;
            overflow: auto;
            color: #333;
            background-color: #fff;
            border-radius: 4px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            box-sizing: border-box;
            margin-bottom: 10px;
        }
        #popup-main-text-area {
            flex: 7;
            overflow-y: auto;
        }
        #popup-additional-text-area {
            flex: 3;
            overflow-y: auto;
        }
#closeButton {
    flex: 0 0 50px;
    margin: 10px 20px;
    font-size: 16px;
    background: linear-gradient(145deg, #6c757d, #343a40); /* Gradient for 3D effect */
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: all 0.3s ease;
    align-self: center;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3), inset 0 2px 4px rgba(0, 0, 0, 0.2); /* 3D shadow effect */
    outline: none; /* Remove default focus outline */
}

#closeButton:hover {
    background: linear-gradient(145deg, #5a6268, #1d2124); /* Slightly darker gradient on hover */
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3), inset 0 1px 3px rgba(0, 0, 0, 0.2); /* Adjust shadow on hover */
}

#closeButton:active {
    background: linear-gradient(145deg, #4e555b, #1d2124); /* Darker gradient on click */
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3), inset 0 1px 2px rgba(0, 0, 0, 0.3); /* Deeper shadow on click */
}

    `;

    const mainTextArea = popupDocument.createElement("div");
    mainTextArea.id = "popup-main-text-area";
    mainTextArea.className = "text-area";
    mainTextArea.contentEditable = true;
    mainTextArea.innerHTML = mainTextAreaContent;

    const additionalTextArea = popupDocument.createElement("div");
    additionalTextArea.id = "popup-additional-text-area";
    additionalTextArea.className = "text-area";
    additionalTextArea.contentEditable = true;
    additionalTextArea.innerHTML = additionalTextAreaContent;

    function syncText() {
        const formatText = (text) => {
            let formattedText = text.replace(/<div><br><\/div>/g, '\n\n');
            formattedText = formattedText.replace(/<div>/g, '');
            formattedText = formattedText.replace(/<\/div>/g, '\n');
            return formattedText;
        };

        updateNoteContent(initialSelectedNoteId, formatText(mainTextArea.innerHTML), formatText(additionalTextArea.innerHTML));
    }

    function handlePaste(event, textArea) {
        event.preventDefault();
        const pastedText = event.clipboardData.getData('text/plain');
        if (pastedText) {
            const textWithLineBreaks = pastedText.replace(/\n/g, '<br>');
            const selection = popupWindow.getSelection();
            const range = selection.getRangeAt(0);
            range.deleteContents();

            const fragment = popupDocument.createDocumentFragment();
            const tempDiv = popupDocument.createElement('div');
            tempDiv.innerHTML = textWithLineBreaks;
            while (tempDiv.firstChild) {
                fragment.appendChild(tempDiv.firstChild);
            }

            range.insertNode(fragment);
            range.collapse(false);
            selection.removeAllRanges();
            selection.addRange(range);
            syncText();
        }
    }

    function handleCopy(event, textArea) {
        event.preventDefault();
        const selection = popupWindow.getSelection();
        const selectedText = selection.toString();
        event.clipboardData.setData('text/plain', selectedText);
    }

    mainTextArea.addEventListener("paste", (event) => handlePaste(event, mainTextArea));
    additionalTextArea.addEventListener("paste", (event) => handlePaste(event, additionalTextArea));
    mainTextArea.addEventListener("copy", (event) => handleCopy(event, mainTextArea));
    additionalTextArea.addEventListener("copy", (event) => handleCopy(event, additionalTextArea));

    const closeButton = popupDocument.createElement("button");
    closeButton.id = "closeButton";
    closeButton.textContent = "Close";

    popupDocument.head.appendChild(style);
    popupDocument.body.appendChild(mainTextArea);
    popupDocument.body.appendChild(additionalTextArea);
    popupDocument.body.appendChild(closeButton);

    function promptBeforeClose(event) {
        event.preventDefault(); // Prevent default behavior
        event.returnValue = ""; // Trigger the prompt
        return ""; // Ensure the prompt is displayed
    }

    popupWindow.addEventListener("beforeunload", promptBeforeClose);

    closeButton.addEventListener("click", function() {
        storeWindowSize(popupWindow);
        popupWindow.close();
    });

    function syncTextAreaHeights() {
        requestAnimationFrame(() => {
            const mainTextArea = popupDocument.getElementById("popup-main-text-area");
            const additionalTextArea = popupDocument.getElementById("popup-additional-text-area");
            additionalTextArea.style.height = `${mainTextArea.clientHeight}px`;
        });
    }

    popupWindow.addEventListener('load', () => {
        syncTextAreaHeights();
        const savedWindowSize = getStoredWindowSize();
        popupWindow.resizeTo(savedWindowSize.width, savedWindowSize.height);
    });

    let resizeTimeout;
    window.addEventListener("resize", () => {
        clearTimeout(resizeTimeout);
        resizeTimeout = setTimeout(syncTextAreaHeights, 500);
    });

    // Call syncText initially
    syncText();
});




    // Add this line to get the original text area element
    const originalTextArea = document.getElementById("text-area");

    // Add this line to get the new text area element
    const additionalTextArea = document.getElementById("additional-text-area");

    // Load content for the additional text area (if needed)
    // For example, you can call a function like loadAdditionalNoteContent().

function getFederalHolidays(year) {
  return [
    new Date(year, 0, 1), // New Year's Day
    dateFns.addDays(dateFns.startOfWeek(dateFns.addMonths(new Date(year, 0, 1), 1), { weekStartsOn: 1 }), 1), // Martin Luther King, Jr. Day (third Monday in January)
    dateFns.addDays(dateFns.startOfWeek(new Date(year, 1, 1), { weekStartsOn: 1 }), 1 * 7 + 1), // Washington's Birthday (third Monday in February)
    dateFns.addDays(dateFns.startOfWeek(new Date(year, 4, 1), { weekStartsOn: 1 }), 1 * 7 + 1), // Memorial Day (last Monday in May)
    new Date(year, 5, 19), // Juneteenth National Independence Day
    new Date(year, 6, 4), // Independence Day
    dateFns.addDays(dateFns.startOfWeek(new Date(year, 8, 1), { weekStartsOn: 1 }), 1 * 7 + 1), // Labor Day (first Monday in September)
    dateFns.addDays(dateFns.startOfWeek(new Date(year, 9, 1), { weekStartsOn: 1 }), 1 * 7 + 1), // Columbus Day (second Monday in October)
    new Date(year, 10, 11), // Veterans' Day
    dateFns.addDays(dateFns.startOfWeek(new Date(year, 10, 1), { weekStartsOn: 1 }), 4 * 7 + 1), // Thanksgiving Day (fourth Thursday in November)
    new Date(year, 11, 25) // Christmas Day
  ];
}

function closeBusinessDayPopup() {
  const popup = document.getElementById("businessDayPopup");
  popup.style.display = "none";
}


// Function to calculate business day and next business day
function calculateBusinessDay(inputId, resultId, nextBusinessDayId, businessDays) {
  var shipDateString = document.getElementById(inputId).value;
  var shipDate = new Date(shipDateString);
  var endDate = getBusinessDate(shipDate, businessDays);
  document.getElementById(resultId).innerText = endDate.toLocaleDateString();

  // Calculate the next business day based on the endDate
  var nextBusinessDay = calculateNextBusinessDate(endDate);
  document.getElementById(nextBusinessDayId).innerText = nextBusinessDay.toLocaleDateString();
}


// Function to calculate business date, considering federal holidays
function getBusinessDate(startDate, businessDays) {
  var count = 0;
  while (businessDays !== 0) {
    startDate.setDate(startDate.getDate() + (businessDays > 0 ? 1 : -1));
    if (isBusinessDay(startDate)) {
      businessDays -= businessDays > 0 ? 1 : -1;
    }
    count++;
  }
  return startDate;
}

// Function to check if a given date is a business day, considering federal holidays
function isBusinessDay(date) {
  var dayOfWeek = date.getDay();
  if (dayOfWeek === 0 || dayOfWeek === 6) {
    return false; // Weekend
  }

  if (isFederalHoliday(date)) {
    return false; // Federal Holiday
  }

  return true; // Business day
}

function formatDate(date) {
  var month = date.getMonth() + 1;
  var day = date.getDate();
  var year = date.getFullYear();

  // Pad single-digit month and day values with a leading zero if necessary
  var formattedMonth = month < 10 ? "0" + month : month;
  var formattedDay = day < 10 ? "0" + day : day;

  return `${formattedMonth}/${formattedDay}/${year}`;
}

// Event listener to open pop-up business day calculator on Alt + C key press
document.addEventListener("keydown", function(event) {
    // Check if Alt + C is pressed
    if (event.altKey && event.key === "c") {
        // Open the pop-up business day calculator
        openBusinessDayCalculator();
    }
});

// Event listener to close pop-up business day calculator on Esc key press
document.addEventListener("keydown", function(event) {
    // Check if Esc is pressed
    if (event.key === "Escape") {
        // Close the pop-up business day calculator
        closeBusinessDayCalculator();
    }
});

// Function to open the business day calculator pop-up
function openBusinessDayCalculator() {
  var popup = document.getElementById("businessDayPopup");
  popup.style.display = "block";
}

// Function to close the pop-up business day calculator
function closeBusinessDayCalculator() {
  var popup = document.getElementById("businessDayPopup");
  popup.style.display = "none";
}


function isWeekend(date) {
    const day = date.getDay();
    return day === 0 || day === 6;
}

// Function to get the nth weekday of a specific month in a given year
function getNthWeekdayOfMonth(year, month, weekday, n) {
  var firstDay = new Date(year, month, 1);
  var dayOfWeek = firstDay.getDay();
  var date = 1 + (weekday - dayOfWeek + 7) % 7; // Find the first occurrence of the weekday
  date += (n - 1) * 7; // Add n weeks

  return new Date(year, month, date);
}

// Function to check if a given date is a US federal holiday
function isFederalHoliday(date) {
  var year = date.getFullYear();

  // Define the holidays for 2024
  var holidays2024 = [
    new Date(2024, 0, 1),   // New Year's Day (January 1st)
    new Date(2024, 0, 15),  // Martin Luther King, Jr. Day (Third Monday in January)
    new Date(2024, 1, 19),  // Washington's Birthday (Third Monday in February)
    new Date(2024, 4, 27),  // Memorial Day (Last Monday in May)
    new Date(2024, 5, 19),  // Juneteenth (June 19th)
    new Date(2024, 6, 4),   // Independence Day (July 4th)
    new Date(2024, 8, 2),   // Labor Day (First Monday in September)
    new Date(2024, 9, 14),  // Columbus Day (Second Monday in October)
    new Date(2024, 10, 11), // Veterans Day (November 11th)
    new Date(2024, 10, 28), // Thanksgiving Day (Fourth Thursday in November)
    new Date(2024, 11, 25)  // Christmas Day (December 25th)
  ];

  // Define the holidays for 2025
  var holidays2025 = [
    new Date(2025, 0, 1),   // New Year's Day (January 1st)
    new Date(2025, 0, 20),  // Martin Luther King, Jr. Day (Third Monday in January)
    new Date(2025, 1, 17),  // Washington's Birthday (Third Monday in February)
    new Date(2025, 4, 26),  // Memorial Day (Last Monday in May)
    new Date(2025, 5, 19),  // Juneteenth (June 19th)
    new Date(2025, 6, 4),   // Independence Day (July 4th)
    new Date(2025, 8, 1),   // Labor Day (First Monday in September)
    new Date(2025, 9, 13),  // Columbus Day (Second Monday in October)
    new Date(2025, 10, 11), // Veterans Day (November 11th)
    new Date(2025, 10, 27), // Thanksgiving Day (Fourth Thursday in November)
    new Date(2025, 11, 25)  // Christmas Day (December 25th)
  ];

  // Choose the correct holidays array based on the year
  var holidays = (year === 2024) ? holidays2024 : (year === 2025 ? holidays2025 : []);

  // Check if the given date matches any federal holiday
  for (var i = 0; i < holidays.length; i++) {
    if (date.getTime() === holidays[i].getTime()) {
      return true;
    }
  }

  return false;
}



function calculateBusinessDate(startDate, days) {
    let currentDate = new Date(startDate);
    let businessDays = 0;

    // Adjust the start date to the next business day if it's a weekend or a federal holiday
    while (isWeekend(currentDate) || isFederalHoliday(currentDate)) {
        currentDate.setDate(currentDate.getDate() + 1);
    }

    while (businessDays < days) {
        currentDate.setDate(currentDate.getDate() + 1);

        // Skip weekends and federal holidays
        while (isWeekend(currentDate) || isFederalHoliday(currentDate)) {
            currentDate.setDate(currentDate.getDate() + 1);
        }

        businessDays++;
    }

    return currentDate;
}


// Function to calculate the next business day, considering federal holidays
function calculateNextBusinessDate(startDate) {
  var nextBusinessDay = new Date(startDate);

  // Move to the next day
  nextBusinessDay.setDate(nextBusinessDay.getDate() + 1);

  // Skip weekends and federal holidays
  while (isWeekend(nextBusinessDay) || isFederalHoliday(nextBusinessDay)) {
    nextBusinessDay.setDate(nextBusinessDay.getDate() + 1);
  }

  return nextBusinessDay;
}


const password = "igloo"; // Set the correct password

function checkPassword() {
    const enteredPassword = prompt("Enter the password:");
    return enteredPassword === password;
}
        
// Apply formatting to the main text area and additional text area
function applyFormatting(format) {
    const textArea = document.getElementById("text-area");
    const additionalTextArea = document.getElementById("additional-text-area");

    if (format === 'insertHorizontalLine') {
        const horizontalLine = document.createElement("hr");
        textArea.appendChild(horizontalLine);
    } else {
        document.execCommand(format, false, null);
    }

    // Save the formatted content to localStorage
    saveNoteContent(textArea, additionalTextArea);
}


// Assuming you have an icon element with the id "insertHorizontalLineIcon"
const insertHorizontalLineIcon = document.getElementById("insertHorizontalLineIcon");
if (insertHorizontalLineIcon) {
    insertHorizontalLineIcon.addEventListener("click", function () {
        applyFormatting("insertHorizontalLine");
    });
}



// Save the notes and current selection to localStorage
let notes = JSON.parse(localStorage.getItem("notes")) || [
    {
        title: "testsave",
        content: "",
        additionalContent: "",  // Add a property for additional content
        timestamp: new Date().toLocaleString(),
        readonly: false
    }
];

let selectedNoteIndex = 0;
let sidebarCollapsed = false;

        function saveNotesToLocalStorage() {
            localStorage.setItem("notes", JSON.stringify(notes));
        }

function alignText(align) {
    document.execCommand("justify" + align);
    saveNoteContent();
}

function formatTimestamp(date) {
    const options = {
        year: 'numeric',
        month: 'long',
        day: 'numeric',
        hour: 'numeric',
        minute: 'numeric',
        second: 'numeric',
        timeZoneName: 'short',
    };

    return new Intl.DateTimeFormat('en-US', options).format(date);
}

        // Update the sidebar note list
function updateNoteList() {
    const noteList = document.querySelector(".note-list ul");
    noteList.innerHTML = "";

    // Sort notes alphabetically by title
    notes.sort((a, b) => a.title.localeCompare(b.title));

    const searchBar = document.getElementById("searchBar");
    searchBar.addEventListener("input", updateNoteList);
    const searchTerm = searchBar.value.toLowerCase(); // Get the search term

    searchBar.value = searchTerm; // Set the search bar value

    notes.forEach((note, index) => {
        if (!searchTerm || note.title.toLowerCase().includes(searchTerm)) {
            const noteItem = document.createElement("li");
            noteItem.classList.add("note-item");
        noteItem.innerHTML = `
            <span class="note-title">${note.title}</span>
            <span class="note-timestamp">${formatTimestamp(new Date(note.timestamp))}</span>
            <span class="icon" onclick="renameNoteItem(${index})"><i class="fas fa-edit"></i></span>
            <span class="icon" onclick="confirmDeleteNoteItem(${index})"><i class="fas fa-trash-alt"></i></span>
        `;
        noteItem.onclick = function () {
            selectNoteItem(this, index);
            selectedNoteIndex = index;
            loadNoteContent();
        };

        if (index === selectedNoteIndex) {
            noteItem.classList.add("selected");
        }

        noteList.appendChild(noteItem);
        }
    });
}


        // Select a note item in the sidebar
        function selectNoteItem(noteItem, index) {
            const noteItems = document.querySelectorAll(".note-item");
            noteItems.forEach(item => item.classList.remove("selected"));
            noteItem.classList.add("selected");
        }

function changeTextSize() {
    const newSize = prompt("Enter new font size (e.g., 12px | Default text size: 3px):");
    if (newSize) {
        document.execCommand("fontSize", false, newSize);
        saveNoteContent();
    }
}

function attachImage() {
    const imageInput = document.getElementById("imageInput");
    const additionalTextArea = document.getElementById("additional-text-area");
    imageInput.click();
}

// Function to insert a horizontal line at the cursor position
function insertHorizontalLine() {
    const textArea = document.getElementById("text-area");

    // Get the current selection and range
    const selection = window.getSelection();
    const range = selection.getRangeAt(0);

    // Check if the cursor is at the end of a line
    const atEndOfLine = range.endContainer.nodeType === Node.ELEMENT_NODE && range.endOffset === range.endContainer.childNodes.length;

    // Create a wrapper div for the horizontal line
    const wrapperDiv = document.createElement("div");

    // Insert the horizontal line with styles
    const horizontalLine = document.createElement("hr");
    horizontalLine.style.margin = "0"; // Remove default margin
    wrapperDiv.appendChild(horizontalLine);

    // Insert the wrapper div at the current cursor position
    range.deleteContents();
    range.insertNode(wrapperDiv);

    // Save the content to localStorage
    saveNoteContent(textArea, additionalTextArea);

    // Remove extra line breaks if the cursor was at the end of a line
    if (atEndOfLine) {
        const nextSibling = wrapperDiv.nextSibling;
        if (nextSibling && nextSibling.nodeType === Node.ELEMENT_NODE) {
            range.setStartBefore(nextSibling);
            range.setEndBefore(nextSibling);
        } else {
            range.setStartAfter(horizontalLine);
            range.setEndAfter(horizontalLine);
        }
        selection.removeAllRanges();
        selection.addRange(range);
    } else {
        // Remove extra line breaks after the horizontal line
        const nextSibling = wrapperDiv.nextSibling;
        if (nextSibling && nextSibling.nodeType === Node.ELEMENT_NODE) {
            const nextNextSibling = nextSibling.nextSibling;
            if (nextNextSibling && nextNextSibling.nodeType === Node.ELEMENT_NODE) {
                nextSibling.parentNode.removeChild(nextNextSibling);
            }
        }
    }
}

// Inside your insertImage function
function insertImage(event) {
    const imageInput = document.getElementById("imageInput");
    const additionalTextArea = document.getElementById("additional-text-area");
    console.log("Inserting image...");
    const imageFile = event.target.files[0];
    if (imageFile) {
        console.log("Image selected:", imageFile.name);
        const reader = new FileReader();
        reader.onload = function (e) {
            console.log("Image loaded:", imageFile.name);
    const imageUrl = e.target.result;
    const imageHtml = `<img class="resizable-image selectable-image" style="max-width: 50%;" src="${imageUrl}" alt="Attached Image" onclick="selectImage(this)">`;
    document.execCommand("insertHTML", false, imageHtml);

    // Save changes to both the main text area and additional text area
    saveNoteContent(textArea, additionalTextArea);

            // Make the inserted image resizable
            const insertedImage = document.querySelector('.resizable-image');
            interact(insertedImage).resizable({
                edges: { left: true, right: true, bottom: true, top: true }
            }).on('resizemove', function (event) {
                const target = event.target;
                const x = (parseFloat(target.getAttribute('data-x')) || 0);
                const y = (parseFloat(target.getAttribute('data-y')) || 0);

                target.style.width = event.rect.width + 'px';
                target.style.height = event.rect.height + 'px';

                target.style.transform = `translate(${x}px, ${y}px)`;

                target.setAttribute('data-x', x);
                target.setAttribute('data-y', y);
            });
        };
        reader.readAsDataURL(imageFile);
    }
}



// Global variable to store the content of the main text area for each note
let noteContents = {};

// Load the content of the selected note
function loadNoteContent() {
    const textArea = document.getElementById("text-area");
    const additionalTextArea = document.getElementById("additional-text-area");
    const currentNote = notes[selectedNoteIndex];

    // Store the current content of the main text area for the previous note
    if (textArea.getAttribute("data-note-index") !== null) {
        const previousNoteIndex = textArea.getAttribute("data-note-index");
        noteContents[previousNoteIndex] = textArea.innerHTML;
    }

    textArea.contentEditable = !currentNote.readonly;
    // Load the content from noteContents if available, otherwise load from currentNote
    textArea.innerHTML = noteContents[selectedNoteIndex] || currentNote.content;

    additionalTextArea.contentEditable = !currentNote.readonly;
    // Check if additionalContent exists before setting innerHTML
    additionalTextArea.innerHTML = currentNote.additionalContent !== undefined
        ? currentNote.additionalContent.replace(/<div>/g, "\n").replace(/<\/div>/g, "") // Convert <div> tags to line breaks
        : '';

    // Update the data-note-index attribute to reflect the currently loaded note
    textArea.setAttribute("data-note-index", selectedNoteIndex.toString());
}




        // Handle real-time changes in the additional text area with debounce
        const handleAdditionalContentChangeDebounced = debounce(handleAdditionalContentChange, 500);

        additionalTextArea.addEventListener("input", handleAdditionalContentChangeDebounced);

        // Function to handle real-time changes in the additional text area
        function handleAdditionalContentChange() {
            // Save changes to both the main text area and additional text area
            notes[selectedNoteIndex].content = textArea.innerHTML;
            notes[selectedNoteIndex].additionalContent = additionalTextArea.innerHTML;
            saveNotesToLocalStorage();
            updateNoteList();
        }

        // Preserve line breaks when pressing Enter in contenteditable div
        additionalTextArea.addEventListener("keydown", function (e) {
            if (e.key === "Enter") {
                document.execCommand("insertHTML", false, "<br><br>");
                e.preventDefault();
            }
        });

        // Event listener for input changes in the additional text area
        additionalTextArea.addEventListener("input", handleAdditionalContentChange);

        // Add a new note
function addNote() {
    const newNote = {
        title: "Z-Untitled Note",
        content: "",
        additionalContent: "",  // Initialize additionalContent
        timestamp: new Date().toLocaleString()
    };
    notes.push(newNote);
    selectedNoteIndex = notes.length - 1;
    saveNotesToLocalStorage();
    updateNoteList();
    loadNoteContent();
    scrollToSelectedNote();
}

function scrollToSelectedNote() {
    const selectedNoteItem = document.querySelector(".note-item.selected");
    if (selectedNoteItem) {
        selectedNoteItem.scrollIntoView({ behavior: "smooth", block: "nearest" });
    }
}

    // Delete a note item (with confirmation prompt)
    function confirmDeleteNoteItem(index) {
        const confirmed = confirm("Are you sure you want to delete this note?");
        if (confirmed) {
            deleteNoteItem(index);
        }
    }

    // Delete a note item
  function confirmDeleteNoteItem(index) {
    const currentNote = notes[index];

    // Function to delete a note item
    function deleteNote() {
      notes.splice(index, 1);
      selectedNoteIndex = Math.max(0, selectedNoteIndex - 1);
      saveNotesToLocalStorage();
      updateNoteList();
      loadNoteContent();
    }

    // Prevent deleting if the note is 'readonly'
    if (currentNote.readonly) {
      const enteredPassword = prompt("Enter the password to delete this note:");
      if (enteredPassword === "igloo") {
        // Password is correct, show delete confirmation prompt
        showDeleteConfirmation(deleteNote);
      } else {
        alert("Incorrect password. The note cannot be deleted.");
      }
    } else {
      // Note is not readonly, show delete confirmation prompt
      showDeleteConfirmation(deleteNote);
    }
  }

// Function to show the delete confirmation prompt
function showDeleteConfirmation(confirmCallback) {
    const notesCount = notes.length;

    if (notesCount === 1) {
        // If there's only one note, delete it directly without showing the confirmation
        confirmCallback();
        return;
    }

    // Add Font Awesome icon for delete in the confirmation prompt
    const deleteConfirmation = document.createElement("div");
    deleteConfirmation.classList.add("delete-confirmation");
    deleteConfirmation.innerHTML = `
        <h3>Are you sure you want to delete this note?</h3>
        <button onclick="confirmDelete()"><i class="fas fa-check"></i> Delete</button>
        <button class="cancel" onclick="cancelDelete()"><i class="fas fa-times"></i> Cancel</button>
    `;
    document.body.appendChild(deleteConfirmation);

    // Display the delete confirmation with a delay for a smooth fade-in effect
    setTimeout(() => {
      deleteConfirmation.style.display = "block";
    }, 50);

    // Function to confirm the delete action
    window.confirmDelete = function () {
        confirmCallback();
        closeDeleteConfirmation(deleteConfirmation);
    };

    // Function to cancel the delete action
    window.cancelDelete = function () {
        closeDeleteConfirmation(deleteConfirmation);
    };
}

// Function to close the delete confirmation and remove the message
function closeDeleteConfirmation(deleteConfirmation) {
    // Apply fade-out animation
    deleteConfirmation.style.animation = "fadeOut 0.3s ease-in-out";
    
    // Wait for the animation to complete before removing the element
    deleteConfirmation.addEventListener("animationend", function () {
        deleteConfirmation.parentNode.removeChild(deleteConfirmation);
    });
}


function renameNoteItem(index) {
  const currentNote = notes[index];

  // Prevent renaming if the note is 'readonly'
  if (currentNote.readonly) {
    alert("You are not allowed to rename this");
    return;
  }

  // Create a custom styled prompt container
  const promptContainer = document.createElement("div");
  promptContainer.className = "custom-prompt";

  // Add input field
  const inputField = document.createElement("input");
  inputField.type = "text";
  inputField.value = currentNote.title;
  promptContainer.appendChild(inputField);

  // Add confirm button
  const confirmButton = document.createElement("button");
  confirmButton.innerText = "Rename";
  confirmButton.onclick = function () {
    const newTitle = inputField.value.trim();
    if (newTitle !== "") {
      currentNote.title = newTitle;
      saveNotesToLocalStorage();
      updateNoteList();

      // Create a custom styled rename confirmation
      const renameConfirmation = document.createElement("div");
      renameConfirmation.classList.add("rename-confirmation");

      const confirmationText = document.createElement("p");
      confirmationText.textContent = `Note renamed to "${newTitle}"`;

      renameConfirmation.appendChild(confirmationText);

      document.body.appendChild(renameConfirmation);

      // Apply animation using CSS styles
      renameConfirmation.style.position = "fixed";
      renameConfirmation.style.top = "50%";
      renameConfirmation.style.left = "50%";
      renameConfirmation.style.transform = "translate(-50%, -50%)";
      renameConfirmation.style.backgroundColor = "#4CAF50"; // Background color
      renameConfirmation.style.color = "#fff"; // Text color
      renameConfirmation.style.padding = "15px"; // Padding
      renameConfirmation.style.borderRadius = "10px"; // Border radius
      renameConfirmation.style.animation = "fadeOut 2s ease-in-out"; // Apply animation

      // Remove the confirmation after 2 seconds (adjust duration as needed)
      setTimeout(() => {
        document.body.removeChild(renameConfirmation);
      }, 2000);
    }

    // Remove the custom prompt container
    document.body.removeChild(promptContainer);
  };
  promptContainer.appendChild(confirmButton);

  // Add cancel button
  const cancelButton = document.createElement("button");
  cancelButton.innerText = "Cancel";
  cancelButton.onclick = function () {
    // Remove the custom prompt container
    document.body.removeChild(promptContainer);
  };
  promptContainer.appendChild(cancelButton);

  // Append the custom prompt container to the body here
  document.body.appendChild(promptContainer);
}



// Save the content of the current note to localStorage
function saveNoteContent() {
    const textArea = document.getElementById("text-area");
    const additionalTextArea = document.getElementById("additional-text-area");

    notes[selectedNoteIndex].content = textArea.innerHTML;
    notes[selectedNoteIndex].additionalContent = additionalTextArea.innerHTML;

    notes[selectedNoteIndex].timestamp = new Date().toISOString(); // Update timestamp to current time

    // Save notes to local storage
    localStorage.setItem("notes", JSON.stringify(notes));

    // Broadcast a message to other tabs about the updated notes content
    localStorage.setItem("notesContent", JSON.stringify({
        selectedNoteIndex: selectedNoteIndex,
        content: textArea.innerHTML,
        additionalContent: additionalTextArea.innerHTML
    }));
}


        // Export notes as a JSON file
        function exportData() {
            const data = JSON.stringify(notes);
            const blob = new Blob([data], {
                type: "application/json"
            });
            const url = URL.createObjectURL(blob);
            const a = document.createElement("a");
            a.href = url;
            a.download = "notes.json";
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        // Open the file import dialog
function openImportDialog() {
    const importInput = document.getElementById("importInput");
    importInput.setAttribute("accept", ".json"); // Specify accepted file format
    importInput.click();
}

// Import notes from a JSON file
function triggerFileInput() {
    const importInput = document.getElementById("importInput");
    importInput.click();
}

let testSavePasswordPrompted = false; // Add this global variable

function importData(event) {
    const file = event.target.files[0];
    if (!file) return;

    const reader = new FileReader();
    reader.onload = function (e) {
        const fileContent = e.target.result;
        if (typeof fileContent !== 'string') {
            alert("Invalid file content. Please select a valid JSON file.");
            return;
        }

        try {
            console.log("File content:", fileContent);
            const importedData = JSON.parse(fileContent);
            console.log("Imported data:", importedData);

            if (!Array.isArray(importedData)) {
                alert("Invalid file format. Please select a valid JSON file.");
                return;
            }

            const isTestSaveFile = file.name === "testsave.json";
            const passwordCorrect = isTestSaveFile && !testSavePasswordPrompted ? checkPassword() : true;

            importedData.forEach(importedNote => {
                const existingNoteIndex = notes.findIndex(note => note.title === importedNote.title);

                if (existingNoteIndex !== -1) {
                    // Update existing note with imported data
                    notes[existingNoteIndex].content = importedNote.content;
                    notes[existingNoteIndex].additionalContent = importedNote.additionalContent;
                    if (isTestSaveFile && (!passwordCorrect || importedNote.readonly)) {
                        notes[existingNoteIndex].readonly = true; // Mark as readonly if password is incorrect or readonly flag is set
                    }
                } else {
                    // Add imported note if it doesn't exist
                    importedNote.readonly = isTestSaveFile && (!passwordCorrect || importedNote.readonly);
                    notes.push(importedNote);
                }
            });

            if (isTestSaveFile) {
                testSavePasswordPrompted = true;

                // Apply readonly status to imported notes in real-time
                notes.forEach((note, index) => {
                    if (note.readonly) {
                        const textArea = document.getElementById("text-area");
                        textArea.setAttribute("contenteditable", "false");
                    }
                });
            }

            saveNotesToLocalStorage();
            updateNoteList();
            loadNoteContent();

            // Update the text area content with the imported note's content
            const importedNote = importedData.find(note => note.title === notes[selectedNoteIndex].title);
            if (importedNote) {
                const textArea = document.getElementById("text-area");
                textArea.innerHTML = importedNote.content;
            }
        } catch (error) {
            console.error("Error parsing JSON file:", error);
            alert("Error parsing JSON file. Please check the console for more details.");
        }
    };

    reader.readAsText(file, "utf-8");
}









        // Variable to store the original width of the text area
        let originalTextAreaWidth;

        // Function to get the original width of the text area
        function getOriginalTextAreaWidth() {
            const textArea = document.getElementById("text-area");
            originalTextAreaWidth = textArea.offsetWidth;
        }

// Function to toggle the collapsed class on the text area and notepad container
function toggleTextAreaWidth() {
    const textArea = document.getElementById("text-area");
    const notepadContainer = document.querySelector(".notepad-container");

    if (sidebarCollapsed) {
        // When the sidebar is collapsed, stretch the text area to cover the entire width
        textArea.style.width = `100%`;
    } else {
        // When the sidebar is not collapsed, restore the original width of the text area
        textArea.style.width = `${originalTextAreaWidth}px`;
    }

    notepadContainer.classList.toggle("collapsed", sidebarCollapsed);
}


// Variable to store the initial viewport width
let initialViewportWidth = window.innerWidth;

// Function to set transition class for animation
function setTransitionClass(element, addClass) {
  element.classList.add("transition");
  addClass();
  setTimeout(() => {
    element.classList.remove("transition");
  }, 300); // Adjust the duration to match your desired animation time
}

// Toggle sidebar visibility
function toggleSidebar() {
  const sidebar = document.querySelector(".sidebar");
  const notepadContainer = document.querySelector(".notepad-container");
  const additionalTextArea = document.getElementById("additional-text-area");

  sidebarCollapsed = !sidebarCollapsed;
  sidebar.classList.toggle("collapsed", sidebarCollapsed);

  if (sidebarCollapsed) {
    setTransitionClass(textArea, () => {
      // Set the width to 96.5% of the initial viewport width for small screens
      const newWidth = window.innerWidth < 790 ? '95vw' : '96.5vw';
      textArea.style.width = newWidth;
      additionalTextArea.style.width = newWidth;
    });
  } else {
    setTransitionClass(textArea, () => {
      textArea.style.width = '100%';
      additionalTextArea.style.width = '100%';
    });
  }

  notepadContainer.classList.toggle("collapsed", sidebarCollapsed);
}

// Update the initialViewportWidth when the window is resized
window.addEventListener('resize', function() {
  initialViewportWidth = window.innerWidth;
});

// Update text area widths on zoom
window.addEventListener('resize', function() {
  if (!sidebarCollapsed) {
    textArea.style.width = '100%';
    additionalTextArea.style.width = '100%';
  }
});


// Function to open the selected image in a new tab
function viewImage(imageUrl) {
    window.open(imageUrl, "_blank");
}

// Define a debounce function to delay the execution of a function
function debounce(func, delay) {
  let timeout;
  return function() {
    const context = this;
    const args = arguments;
    clearTimeout(timeout);
    timeout = setTimeout(() => {
      func.apply(context, args);
    }, delay);
  };
}


// Load initial notes and content
document.addEventListener("DOMContentLoaded", () => {
    initializeApp();
});

function initializeApp() {
    updateNoteList();
    loadNoteContent();
    getOriginalTextAreaWidth();
    updateNotesFromLocalStorage();
    setupEventListeners();
}

// Update notes from localStorage on page load or when changes are detected in other tabs
function updateNotesFromLocalStorage() {
    const storedNotes = JSON.parse(localStorage.getItem("notes"));
    if (!storedNotes) return;

    notes = storedNotes;
    updateNoteList();
    loadNoteContent();

    const notesContent = JSON.parse(localStorage.getItem("notesContent"));
    const textArea = document.getElementById("text-area");
    const additionalTextArea = document.getElementById("additional-text-area");

    if (notesContent && notesContent.selectedNoteIndex === selectedNoteIndex) {
        textArea.innerHTML = notesContent.content;
        additionalTextArea.innerHTML = notesContent.additionalContent;
    } else {
        textArea.innerHTML = notes[selectedNoteIndex].content;
        additionalTextArea.innerHTML = notes[selectedNoteIndex].additionalContent;
    }
}

// Set up event listeners
function setupEventListeners() {
    const textArea = document.getElementById("text-area");
    const additionalTextArea = document.getElementById("additional-text-area");
    const importInput = document.getElementById("importInput");

    const saveNoteContentDebounced = debounce(saveNoteContent, 500);

    textArea.addEventListener("input", saveNoteContentDebounced);
    additionalTextArea.addEventListener("input", saveNoteContentDebounced);
    textArea.addEventListener("paste", handlePaste);
    additionalTextArea.addEventListener("paste", handlePaste);
    importInput.addEventListener("change", importData);

    // Listen for storage changes across tabs
    window.addEventListener("storage", handleStorageChange);
}

// Handle paste events to format text
function handlePaste(event) {
    event.preventDefault();

    const text = event.clipboardData.getData("text/plain");
    const formattedText = text.replace(/\n/g, '<br>');
    document.execCommand("insertHTML", false, formattedText);

    saveNoteContent();
}

// Handle storage changes across tabs
function handleStorageChange(event) {
    const textArea = document.getElementById("text-area");
    const additionalTextArea = document.getElementById("additional-text-area");

    if (event.key === "notesContent") {
        const notesContent = JSON.parse(event.newValue);
        if (notesContent.selectedNoteIndex !== selectedNoteIndex) {
            notes[notesContent.selectedNoteIndex].content = notesContent.content;
            notes[notesContent.selectedNoteIndex].additionalContent = notesContent.additionalContent;
        } else {
            textArea.innerHTML = notesContent.content;
            additionalTextArea.innerHTML = notesContent.additionalContent;
        }
    } else if (event.key === "notes") {
        updateNotesFromLocalStorage();
    } else if (event.key === "textAreaContent") {
        textArea.innerHTML = event.newValue;
    } else if (event.key === "additionalTextAreaContent") {
        additionalTextArea.innerHTML = event.newValue;
    }
}

// Debounce function to delay execution
function debounce(func, delay) {
    let timeout;
    return function(...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func.apply(this, args), delay);
    };
}

// Function to format a timestamp for display
function formatTimestamp(timestamp) {
    try {
        return new Date(timestamp).toLocaleString();
    } catch (error) {
        console.error("Error formatting timestamp:", error);
        return "Invalid Timestamp";
    }
}



    </script>
</body>

</html>
