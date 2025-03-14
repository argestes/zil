# CTD (Cihaz Tanımlama Dosyası) Viewer Specification

## 1. Overview
Modern SPA application for viewing and managing CTD (Cihaz Tanımlama Dosyası) documents with secure authentication.

## 2. Technology Stack
- Next.js (App Router)
- Radix UI for components
- TailwindCSS for styling
- XML Parser (fast-xml-parser or similar)

## 3. Authentication & Security
- `.approval` file based authentication
  - Location: Project root
  - Content: Owner name and signature
  - TODO: Implement digital signature verification system
  - TODO: Consider using public/private key pair for document signing

## 4. Core Features

### 4.1 Document Management
- Upload CTD files
- Validate against DTD
- Parse and display in structured format
- Export capabilities (PDF, XML)

### 4.2 UI Components
- Navigation
  - File browser
  - Recent documents
  - Favorites
- Document Viewer
  - Tree view of XML structure
  - Visual representation of terminals
  - Interactive pin/terminal diagram
- Terminal Details Panel
  - Electrical specifications
  - Connected components
  - Notes and warnings

### 4.3 Visual Features
- Interactive terminal diagram
- Color-coded voltage levels
- Connection path visualization
- Component relationship diagrams

## 5. Data Structure

### 5.1 Document Storage
```typescript
interface CTDDocument {
  id: string;
  fileName: string;
  content: string; // XML content
  metadata: {
    createdAt: Date;
    modifiedAt: Date;
    owner: string;
    signature?: string; // TODO: Implement document signing
  };
  validation: {
    isValid: boolean;
    errors?: string[];
  };
}
```

### 5.2 User Preferences
```typescript
interface UserPreferences {
  theme: 'light' | 'dark';
  defaultView: 'tree' | 'diagram';
  recentDocuments: string[]; // Document IDs
  favorites: string[]; // Document IDs
}
```

## 6. API Routes

### 6.1 Document Management
```
POST   /api/documents/upload
GET    /api/documents/[id]
PUT    /api/documents/[id]
DELETE /api/documents/[id]
GET    /api/documents/validate
```

### 6.2 Authentication
```
POST   /api/auth/verify
GET    /api/auth/status
```

## 7. Directory Structure
```
ctd-viewer/
├── .approval           # Authentication file
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   └── (routes)/
│       ├── viewer/
│       └── settings/
├── components/
│   ├── ui/            # Radix UI components
│   ├── viewer/        # CTD specific components
│   └── diagrams/      # Visual representations
├── lib/
│   ├── auth/          # Authentication logic
│   ├── parser/        # XML parsing utilities
│   └── validation/    # DTD validation
└── public/
    └── dtd/           # DTD files
```

## 8. Security Considerations
- Validate all XML input
- Implement rate limiting
- Secure file upload handling
- Document signing verification
- Access control based on .approval file

## 9. Future Enhancements
- Real-time collaboration
- Version control for documents
- Export to different formats
- Mobile responsive design
- Integration with hardware debugging tools

## 10. Development Phases

### Phase 1: Foundation
- Project setup
- Basic authentication
- File upload and validation

### Phase 2: Core Features
- Document viewer
- Terminal visualization
- Basic editing capabilities

### Phase 3: Enhanced Features
- Document signing
- Export functionality
- Advanced visualizations

### Phase 4: Polish
- UI/UX improvements
- Performance optimization
- Documentation
