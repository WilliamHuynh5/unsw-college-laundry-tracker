"A stupid mf is a dumbass who doesn't learn from their failure." -Confucius

# Introduction
The college accommodation laundry tracker is a web-based application that allows students living in college accommodation to keep track of the college's laundry machines. The application will allow students to view the availability of washing machines in their accommodation, and book a time slot to use them.

Supported colleges will be New College and Shalom.

## User interface
The college accommodation laundry tracker will have a simple and intuitive user interface. It will have a login page where students can enter their college accommodation details and login to their account. Once logged in, students will be able to see a calendar view of the washing machine and dryer availability in their accommodation. They will be able to select a time slot and book it for their laundry. 

## Features
- Login page for students to access their account
- View the availbility of laundry machines
- Ability to book a time slot for a laundry machine
- Ability to follow a laundry machine, and recieve email notifications when it is available.
- Send notifications when a laundry machine is available

## Type Interface

<table>
  <tr>
    <th>Variable name</th>
    <th>Type</th>
  </tr>
  <tr>
    <td>has suffix <b>id</b></td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>named exactly <b>booking</b></td>
    <td>Object containing email, booking_date</td>
  </tr>
  <tr>
    <td>has suffix <b>bookings</b></td>
    <td>Array of objects, where each object contains types of <b>booking<b/></td>
  </tr>
  <tr>
    <td>named exactly <b>machine</b></td>
    <td>Object containing <i>machine_id, current_status, bookings </td>
  </tr>
  <tr>
    <td>has suffix <b>machines</b></td>
    <td>Array of objects, where each object contains types of <b>machine<b/></td>
  </tr>
<table/>


## Function Interface

<table>
  <tr>
    <th>Name & Description</th>
    <th>HTTP Method</th>
    <th style="width:18%">Data Types</th>
    <th style="width:32%">Exceptions</th>
  </tr>
  <tr>
    <td><code>auth/login</code><br /><br />Given a registered user's <code>email</code> and <code>password</code>, returns their <code>authUserId</code> value.</td>
    <td style="font-weight: bold; color: blue;">POST</td>
    <td><b>Body Parameters:</b><br /><code>( email, password )</code><br /><br /><b>Return type if no error:</b><br /><code>{ token, authUserId }</code></td>
    <td>
      <b>400 Error</b> when any of:
      <ul>
        <li><code>email</code> entered does not belong to a user</li>
        <li><code>password</code> is not correct</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td><code>auth/register</code><br /><br />Given a user's first and last name, email address, and password, creates a new account for them and returns a new <code>authUserId</code>.
    </td>
    <td style="font-weight: bold; color: blue;">POST</td>
    <td><b>Body Parameters:</b><br /><code>( email, password, nameFirst, nameLast )</code><br /><br /><b>Return type if no error:</b><br /><code>{ token, authUserId }</code></td>
    <td>
      <b>400 Error</b> when any of:
      <ul>
        <li><code>email</code> entered is not a valid email</li>
        <li><code>email</code> is already being used by another user</li>
        <li>length of <code>password</code> is less than 6 characters</li>
        <li>length of <code>nameFirst</code> is not between 1 and 50 characters inclusive</li>
        <li>length of <code>nameLast</code> is not between 1 and 50 characters inclusive</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td><code>auth/logout</code><br /><br />Given an active token, invalidates the token to log the user out.</td>
    <td style="font-weight: bold; color: blue;">POST</td>
    <td><b>Body Parameters:</b><br /><code>{ }</code><br /><br /><b>Return type if no error:</b><br /><code>{}</code></td>
    <td>N/A</td>
  </tr>
  <tr>
    <td><code>laundry/get_availability</code><br /><br />Returns the availability of all laundry machines for a specific date.</td>
    <td style="font-weight: bold; color: blue;">GET</td>
    <td><b>Body Parameters:</b><br /><code>( date )</code><br /><br /><b>Return type if no error:</b><br /><code>{ laundry_machines }</code></td>
    <td>
      <b>400 Error</b> when:
      <ul>
        <li><code>date</code> provided is invalid</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td><code>laundry/book</code><br /><br />Books a laundry machine for a specific date time.</td>
    <td style="font-weight: bold; color: blue;">POST</td>
    <td><b>Body Parameters:</b><br /><code>( laundry_machine_id, date )</code><br /><br /><b>Return type if no error:</b><br /><code>{ booking_id }</code></td>
    <td>
      <b>400 Error</b> when:
      <ul>
        <li><code>laundry_machine_id</code> provided is invalid</li>
        <li><code>date</code> provided is invalid</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td><code>laundry/unbook</code><br /><br />Unbooks a laundry machine given a booking_id</td>
    <td style="font-weight: bold; color: blue;">POST</td>
    <td><b>Body Parameters:</b><br /><code>( booking_id )</code><br /><br /><b>Return type if no error:</b><br /><code>{ }</code></td>
    <td>
      <b>400 Error</b> when:
      <ul>
        <li><code>booking_id</code> provided is invalid</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td><code>laundry/follow</code><br /><br />Follows a laundry machine given its Id. Allows the user to recieve notifications when this particular laundry machine is available.</td>
    <td style="font-weight: bold; color: blue;">POST</td>
    <td><b>Body Parameters:</b><br /><code>( laundry_machine_id, date )</code><br /><br /><b>Return type if no error:</b><br /><code>{ }</code></td>
    <td>
      <b>400 Error</b> when:
      <ul>
        <li><code>laundry_machine_id</code> provided is invalid</li>
      </ul>
    </td>
  </tr>
    <tr>
    <td><code>laundry/unfollow</code><br /><br />Unfollows a laundry machine given its Id. Allows the user to recieve notifications when this particular laundry machine is available.</td>
    <td style="font-weight: bold; color: blue;">POST</td>
    <td><b>Body Parameters:</b><br /><code>( laundry_machine_id, date )</code><br /><br /><b>Return type if no error:</b><br /><code>{ }</code></td>
    <td>
      <b>400 Error</b> when:
      <ul>
        <li><code>laundry_machine_id</code> provided is invalid</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td><code>notification/send</code><br /><br />Sends a notification to the user's email address when a laundry machine in a user's list of followed laundry machines is available.</td>
    <td style="font-weight: bold; color: blue;">POST</td>
    <td><b>Body Parameters:</b><br /><code>( laundry_machine_id, email )</code><br /><br /><b>Return type if no error:</b><br /><code>{ }</code></td>
    <td>
      <b>400 Error</b> when:
      <ul>
        <li><code>laundry_machine_id</code> provided is invalid</li>
        <li><code>email</code> provided is invalid</li>
      </ul>
    </td>
  </tr>
