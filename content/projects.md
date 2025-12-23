---
title: "Dự Án"
layout: "single"
url: "/projects/"
summary: "Các dự án của tôi"
ShowToc: false
ShowBreadCrumbs: true
---

<style>
.project-card {
    background: linear-gradient(135deg, rgba(30, 30, 46, 0.7), rgba(24, 24, 37, 0.9));
    border-left: 4px solid #89b4fa;
    border-radius: 12px;
    padding: 25px;
    margin-bottom: 30px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.project-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 20px rgba(137, 180, 250, 0.2);
}

.project-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 15px;
    flex-wrap: wrap;
    gap: 10px;
}

.project-title {
    font-size: 1.5em;
    font-weight: bold;
    color: #cdd6f4;
    margin: 0;
    flex: 1;
}

.project-status {
    background: #a6e3a1;
    color: #1e1e2e;
    padding: 5px 15px;
    border-radius: 20px;
    font-size: 0.85em;
    font-weight: 600;
    white-space: nowrap;
}

.project-status.in-progress {
    background: #f9e2af;
}

.project-status.paused {
    background: #f38ba8;
}

.project-description {
    color: #bac2de;
    line-height: 1.7;
    margin-bottom: 20px;
}

.project-section {
    margin-bottom: 15px;
}

.project-section h4 {
    color: #89b4fa;
    font-size: 1em;
    margin-bottom: 8px;
    font-weight: 600;
}

.project-section ul {
    margin: 0;
    padding-left: 20px;
    color: #cdd6f4;
}

.project-section ul li {
    margin-bottom: 5px;
}

.tech-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 8px;
}

.tech-tag {
    background: rgba(137, 180, 250, 0.15);
    color: #89b4fa;
    padding: 5px 12px;
    border-radius: 6px;
    font-size: 0.85em;
    border: 1px solid rgba(137, 180, 250, 0.3);
}

.section-header {
    margin-top: 40px;
    margin-bottom: 30px;
    padding-bottom: 10px;
    border-bottom: 2px solid #89b4fa;
}
</style>

<div id="main"></div>

<div class="section-header">
<h2>🔐 Main Projects</h2>
<p style="color: #bac2de;">Các dự án chính tập trung về An ninh mạng và Cybersecurity</p>
</div>

<div class="project-card">
    <div class="project-header">
        <h3 class="project-title">Khai thác và đánh giá lỗ hổng của ứng dụng web theo chuẩn OWASP</h3>
        <span class="project-status">✓ Hoàn thành</span>
    </div>
    <p class="project-description">
        Xây dựng một ứng dụng web thương mại điện tử có chủ đích tồn tại các lỗ hổng bảo mật nhằm mô phỏng quy trình kiểm thử xâm nhập thực tế. Dự án tập trung vào việc phát hiện, khai thác và vá các lỗ hổng phổ biến theo OWASP Top 10.
    </p>
    <div class="project-section">
        <h4>🎯 Mục tiêu</h4>
        <ul>
            <li>Đánh giá mức độ an toàn của ứng dụng web</li>
            <li>Phát hiện và khai thác các lỗ hổng phổ biến trong thực tế</li>
            <li>Hiểu rõ nguyên nhân gây lỗi và cách phòng chống</li>
        </ul>
    </div>
    <div class="project-section">
        <h4>🔍 Phạm vi lỗ hổng</h4>
        <ul>
            <li><strong>SQL Injection (SQLi)</strong> - Tấn công cơ sở dữ liệu</li>
            <li><strong>Cross-Site Scripting (XSS)</strong> - Chèn mã độc JavaScript</li>
            <li><strong>Broken Access Control</strong> - Kiểm soát truy cập không an toàn</li>
        </ul>
    </div>
    <div class="project-section">
        <h4>🛠️ Công nghệ sử dụng</h4>
        <div class="tech-tags">
            <span class="tech-tag">Burp Suite</span>
            <span class="tech-tag">PHP / Laravel</span>
            <span class="tech-tag">MySQL</span>
        </div>
    </div>
    <div class="project-section">
        <h4>✨ Kết quả đạt được</h4>
        <ul>
            <li>Khai thác thành công 3 nhóm lỗ hổng chính</li>
            <li>Thực hiện vá lỗi và kiểm tra lại sau khi khắc phục</li>
            <li>Nắm vững quy trình penetration testing thực tế</li>
        </ul>
    </div>
</div>

<div class="project-card">
    <div class="project-header">
        <h3 class="project-title">Xây dựng hệ thống giám sát an toàn thông tin doanh nghiệp</h3>
        <span class="project-status">✓ Hoàn thành</span>
    </div>
    <p class="project-description">
        Triển khai hệ thống giám sát an toàn thông tin mô phỏng môi trường doanh nghiệp nhằm thu thập log, phát hiện tấn công và phản ứng tự động trước các mối đe dọa phổ biến trong mạng nội bộ.
    </p>
    <div class="project-section">
        <h4>🖥️ Môi trường & Công nghệ</h4>
        <ul>
            <li><strong>Virtualization:</strong> VMware Workstation</li>
            <li><strong>Network Security:</strong> pfSense Firewall</li>
            <li><strong>Operating Systems:</strong> Windows Server 2022, Ubuntu Linux, Kali Linux</li>
            <li><strong>SIEM Platform:</strong> Wazuh (All-in-One), ELK Stack</li>
        </ul>
    </div>
    <div class="project-section">
        <h4>🔬 Nội dung chính</h4>
        <ul>
            <li>Thu thập và phân tích log tập trung từ các máy trong hệ thống</li>
            <li>Thử nghiệm tấn công brute-force và thả file mã độc giả lập</li>
            <li>Kích hoạt cơ chế Active Response để tự động phòng thủ</li>
        </ul>
    </div>
    <div class="project-section">
        <h4>🛠️ Công nghệ sử dụng</h4>
        <div class="tech-tags">
            <span class="tech-tag">VMware</span>
            <span class="tech-tag">pfSense</span>
            <span class="tech-tag">Windows Server</span>
            <span class="tech-tag">Wazuh</span>
            <span class="tech-tag">ELK Stack</span>
            <span class="tech-tag">Kali Linux</span>
        </div>
    </div>
    <div class="project-section">
        <h4>✨ Kết quả đạt được</h4>
        <ul>
            <li>Phát hiện thành công các hành vi tấn công thử nghiệm</li>
            <li>Giảm rủi ro nhờ phản ứng tự động theo rule</li>
            <li>Xây dựng được môi trường giám sát an toàn thông tin hoàn chỉnh</li>
        </ul>
    </div>
    <div class="project-section">
        <h4>🚀 Định hướng phát triển</h4>
        <ul>
            <li>Nghiên cứu tích hợp Machine Learning (Isolation Forest) để phát hiện bất thường</li>
            <li>Mở rộng quy mô hệ thống với nhiều node hơn</li>
        </ul>
    </div>
</div>

---

<div id="side"></div>

<div class="section-header">
<h2>💻 Side Projects</h2>
<p style="color: #bac2de;">Các dự án phụ và thử nghiệm công nghệ</p>
</div>

<div class="project-card">
    <div class="project-header">
        <h3 class="project-title">Khai thác tập mục ẩn có độ chiếm dụng hữu ích cao</h3>
        <span class="project-status in-progress">🔬 Research</span>
    </div>
    <p class="project-description">
        Nghiên cứu lý thuyết dựa trên thuật toán HHUIF (High Hiding Utility Itemsets Framework), đề xuất cải tiến nhằm tối ưu quá trình ẩn dữ liệu nhạy cảm trong khai phá dữ liệu.
    </p>
    <div class="project-section">
        <h4>🎯 Mục tiêu</h4>
        <ul>
            <li>Nghiên cứu và phân tích thuật toán HHUIF</li>
            <li>Đề xuất cải tiến để tối ưu hiệu suất ẩn dữ liệu</li>
            <li>Bảo vệ thông tin nhạy cảm trong khai phá dữ liệu</li>
        </ul>
    </div>
    <div class="project-section">
        <h4>🛠️ Lĩnh vực</h4>
        <div class="tech-tags">
            <span class="tech-tag">Data Mining</span>
            <span class="tech-tag">Algorithm Design</span>
            <span class="tech-tag">Research</span>
        </div>
    </div>
</div>

<div class="project-card">
    <div class="project-header">
        <h3 class="project-title">E-commerce Website (Sportswear)</h3>
        <span class="project-status">✓ Hoàn thành</span>
    </div>
    <p class="project-description">
        Xây dựng website thương mại điện tử chuyên về trang phục thể thao với đầy đủ chức năng quản lý sản phẩm, giỏ hàng, thanh toán và quản trị hệ thống.
    </p>
    <div class="project-section">
        <h4>🛠️ Công nghệ sử dụng</h4>
        <div class="tech-tags">
            <span class="tech-tag">ASP.NET</span>
            <span class="tech-tag">Microsoft SQL Server</span>
            <span class="tech-tag">C#</span>
        </div>
    </div>
</div>

<div class="project-card">
    <div class="project-header">
        <h3 class="project-title">TOEIC Practice Mobile App</h3>
        <span class="project-status">✓ Hoàn thành</span>
    </div>
    <p class="project-description">
        Ứng dụng mobile hỗ trợ luyện thi TOEIC với các bài tập, đề thi thử và theo dõi tiến độ học tập.
    </p>
    <div class="project-section">
        <h4>🛠️ Công nghệ sử dụng</h4>
        <div class="tech-tags">
            <span class="tech-tag">Flutter</span>
            <span class="tech-tag">Dart</span>
            <span class="tech-tag">Mobile Development</span>
        </div>
    </div>
</div>
