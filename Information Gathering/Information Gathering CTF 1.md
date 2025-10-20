Completing Skill Check Labs
    Skill Check Labs are interactive, hands-on exercises designed to validate the knowledge and skills you’ve gained in this course through real-world scenarios. Each lab presents practical tasks that require you to apply what you’ve learned. Unlike other INE labs, solutions are not provided, challenging you to demonstrate your understanding and problem-solving abilities. Your performance is graded, allowing you to track progress and measure skill growth over time.

Lab Environment
A website is accessible at http://target.ine.local. Perform reconnaissance and capture the following flags.

    Flag 1: This tells search engines what to and what not to avoid.
    Flag 2: What website is running on the target, and what is its version?
    Flag 3: Directory browsing might reveal where files are stored.
    Flag 4: An overlooked backup file in the webroot can be problematic if it reveals sensitive configuration details.
    Flag 5: Certain files may reveal something interesting when mirrored.
Tools
    Firefox
    Curl
    HTTrack

- Flag1: This tells search engines what to and what not to avoid.
Đơn giản chỉ cần truy cập http://target.ine.local/robots.txt để lấy flag.

- Flag2: What website is running on the target, and what is its version?
Sử dụng nmap
```bash
nmap target.ine.local -sC -sV 
```


