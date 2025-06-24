# temp


"You are a software library classifier. Choose the most relevant category for the given library description from the list below. Return only the category name — no explanation."


def make_llama_prompt(description):
    return f"""
You are a software classifier.

Choose the **most relevant** category from the following list. Return only the exact category name.

Categories:
- JSON
- Database
- Web
- Security
- Logging and Monitoring
- Testing
- Build-tools
- UI
- ML
- Data Processing
- Networking
- File-Handling
- Image Processing
- Audio Processing
- Video Processing
- Cloud
- Containerization
- DevOps
- Search
- Cryptography
- Compression
- Math
- Utilities

Examples:

Description: Parses JSON into Java objects using the Jackson library.
Category: JSON

Description: Runs SQL queries using JDBC for accessing relational databases.
Category: Database

Description: Provides secure authentication with OAuth2 in a Spring Boot app.
Category: Security

Description: Adds unit testing support using JUnit and Mockito.
Category: Testing

Description: Offers utilities for encoding and decoding Base64 strings.
Category: Utilities

Now classify this:

Description: {description}
Category:"""
