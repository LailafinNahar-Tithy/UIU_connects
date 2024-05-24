<h1> UIU_Connect    </h1>
 This project is a web application designed to connect university students and faculty members. It allows users to create profiles, share information, post events, apply for jobs, and generate CVs.




## Database for our project
<a href="https://laravel.com/docs/10.x/readme">Click here to read Laravel Documentation</a>
>We have to use make models for each table with the following command so we can have migration files at the same time. 
`Model name is basically the name of the table.`
```
php artisan make:model [modelname] -m
```
>run this command to see helping commands while making model 
```
php artisan make:model --help 
```
<hr>

```sql
CREATE DATABASE university_connect;

USE university_connect;

CREATE TABLE `users` (
    `u_id` bigint(20) UNSIGNED NOT NULL,
    `username` varchar(50) COLLATE utf8mb4_unicode_ci NOT NULL,
    `password` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `email` varchar(50) COLLATE utf8mb4_unicode_ci NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

CREATE TABLE jobs (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    user_id INT UNSIGNED NOT NULL,
    job_title VARCHAR(255) NOT NULL,
    job_description TEXT,
    application_info TEXT,
    time_limitation INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE job_applications (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    job_id INT UNSIGNED NOT NULL,
    user_id INT UNSIGNED NOT NULL,
    cv_path VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (job_id) REFERENCES jobs(id),
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE events (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    user_id INT UNSIGNED NOT NULL,
    event_title VARCHAR(255) NOT NULL,
    event_date DATE,
    event_time TIME,
    event_location VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE posts (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    user_id INT UNSIGNED NOT NULL,
    post_content TEXT NOT NULL,
    post_category ENUM('general', 'job', 'event') NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE cv_templates (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    template_name VARCHAR(255) NOT NULL,
    template_format VARCHAR(255) NOT NULL,
    template_path VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);


CREATE TABLE `awards` (
    `awd_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `award_name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `date_received` date NOT NULL,
    `description` text COLLATE utf8mb4_unicode_ci NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- --------------------------------------------------------

--
-- Table structure for table `certifications`
--

CREATE TABLE `certifications` (
    `cert_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `certification_name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `issuing_organization` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `credentials` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `expiration_date` date NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- --------------------------------------------------------

--
-- Table structure for table `contacts`
--

CREATE TABLE `contacts` (
    `c_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `name` varchar(50) COLLATE utf8mb4_unicode_ci NOT NULL,
    `email` varchar(50) COLLATE utf8mb4_unicode_ci NOT NULL,
    `phone` varchar(25) COLLATE utf8mb4_unicode_ci NOT NULL,
    `message` text COLLATE utf8mb4_unicode_ci NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- --------------------------------------------------------

--
-- Table structure for table `education`
--

CREATE TABLE `education` (
    `ed_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `institution` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `degree` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `field_of_study` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `graduation_date` date NOT NULL,
    `description` text COLLATE utf8mb4_unicode_ci NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- --------------------------------------------------------

--
-- Table structure for table `experiences`
--

CREATE TABLE `experiences` (
    `e_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `company` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `position` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `start_date` date NOT NULL,
    `end_date` date DEFAULT NULL,
    `description` text COLLATE utf8mb4_unicode_ci NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;



CREATE TABLE `interests` (
    `i_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `interest_name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `date_received` date NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;




CREATE TABLE `personalinfos` (
    `pinfo_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `fathersName` varchar(50) COLLATE utf8mb4_unicode_ci NOT NULL,
    `mothersName` varchar(50) COLLATE utf8mb4_unicode_ci NOT NULL,
    `image_path` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `dob` date NOT NULL,
    `nationalId` varchar(100) COLLATE utf8mb4_unicode_ci NOT NULL,
    `address` text COLLATE utf8mb4_unicode_ci NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;



CREATE TABLE `projects` (
    `p_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `project_name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `description` text COLLATE utf8mb4_unicode_ci NOT NULL,
    `start_date` date NOT NULL,
    `end_date` date DEFAULT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;



CREATE TABLE `publications` (
    `pub_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `publisher` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `publication_date` date NOT NULL,
    `link` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `citation` text COLLATE utf8mb4_unicode_ci NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;



CREATE TABLE `skills` (
    `sk_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `skill_name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `proficiency` int(11) NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- --------------------------------------------------------


CREATE TABLE `testimonials` (
    `te_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `source` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `date_received` date NOT NULL,
    `phone` varchar(25) COLLATE utf8mb4_unicode_ci NOT NULL,
    `quote` text COLLATE utf8mb4_unicode_ci NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- --------------------------------------------------------




CREATE TABLE `volunteer_works` (
    `vol_id` bigint(20) UNSIGNED NOT NULL,
    `user_id` bigint(20) UNSIGNED NOT NULL,
    `organization` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
    `role` varchar(100) COLLATE utf8mb4_unicode_ci NOT NULL,
    `start_date` date NOT NULL,
    `end_date` date NOT NULL,
    `description` text COLLATE utf8mb4_unicode_ci NOT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

--we need comments tables or others types like this
