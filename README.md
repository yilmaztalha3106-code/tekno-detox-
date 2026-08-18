# tekno-detox-import SwiftUI

// --- 1. MODEL VE DURUM YÖNETİMİ ---
class UserState: ObservableObject {
    @Published var name: String = "Siber Savaşçı"
    @Published var trophies: Int = 18
    @Published var xp: Int = 1250
    @Published var clubName: String = "Kod Avcıları"
    @Published var selectedAvatar: String = "🤖"
}

struct Question {
    let text: String
    let options: [String]
    let correctAnswer: Int
}

struct Course: Identifiable {
    let id = UUID()
    let title: String
    let xpReward: Int
    var isCompleted: Bool = false
}

// --- 2. ANA UYGULAMA YAPISI ---
struct ContentView: View {
    @StateObject private var user = UserState()
    @State private var selectedTab = 0
    
    var body: some View {
        TabView(selection: $selectedTab) {
            HomeArenaView(user: user)
                .tabItem {
                    Label("Arena", systemImage: "bolt.fill")
                }
                .tag(0)
            
            AcademyView(user: user)
                .tabItem {
                    Label("Dersler", systemImage: "book.fill")
                }
                .tag(1)
            
            LeaderboardView(user: user)
                .tabItem {
                    Label("Sıralama", systemImage: "trophy.fill")
                }
                .tag(2)
        }
        .accentColor(.orange)
        .preferredColorScheme(.dark)
    }
}

// --- 3. ANA SAYFA & CANLI ARENA EKRANI ---
struct HomeArenaView: View {
    @ObservedObject var user: UserState
    @State private var isSearchingMatch = false
    @State private var showQuiz = false
    
    var body: some View {
        NavigationView {
            VStack(spacing: 25) {
                // Profil & Karakter Kartı
                VStack(spacing: 15) {
                    Text(user.selectedAvatar)
                        .font(.system(size: 60))
                        .padding()
                        .background(
                            Circle()
                                .fill(Color.orange.opacity(0.2))
                                .shadow(color: .orange.opacity(0.4), radius: 10)
                        )
                    
                    Text(user.name)
                        .font(.title2)
                        .bold()
                    
                    Text("🛡️ \(user.clubName)")
                        .font(.subheadline)
                        .foregroundColor(.gray)
                    
                    HStack(spacing: 20) {
                        HStack {
                            Image(systemName: "trophy.fill")
                                .foregroundColor(.yellow)
                            Text("\(user.trophies) Kupa")
                                .bold()
                        }
                        .padding(.horizontal, 12)
                        .padding(.vertical, 6)
                        .background(Color.yellow.opacity(0.15))
                        .cornerRadius(12)
                        
                        HStack {
                            Image(systemName: "star.fill")
                                .foregroundColor(.cyan)
                            Text("\(user.xp) XP")
                                .bold()
                        }
                        .padding(.horizontal, 12)
                        .padding(.vertical, 6)
                        .background(Color.cyan.opacity(0.15))
                        .cornerRadius(12)
                    }
                }
                .padding()
                .frame(maxWidth: .infinity)
                .background(RoundedRectangle(cornerRadius: 24).fill(Color(.systemGray6)))
                
                Spacer()
                
                // Oyna Butonu
                Button(action: {
                    isSearchingMatch = true
                }) {
                    HStack {
                        Image(systemName: "play.fill")
                        Text("CANLI 5 KİŞİLİK ARENA")
                            .bold()
                    }
                    .font(.headline)
                    .foregroundColor(.white)
                    .frame(maxWidth: .infinity)
                    .padding()
                    .background(
                        LinearGradient(colors: [.orange, .red], startPoint: .leading, endPoint: .trailing)
                    )
                    .cornerRadius(30)
                    .shadow(color: .orange.opacity(0.4), radius: 10)
                }
                .sheet(isPresented: $isSearchingMatch) {
                    MatchmakingView(user: user, isSearching: $isSearchingMatch)
                }
                
                Spacer()
            }
            .padding()
            .navigationTitle("Karakter & Arena")
        }
    }
}

// --- 4. 5 KİŞİLİK EŞLEŞME & YARIŞMA LOBİSİ ---
struct MatchmakingView: View {
    @ObservedObject var user: UserState
    @Binding var isSearching: Bool
    @State private var playerCount = 1
    @State private var gameStarted = false
    let timer = Timer.publish(every: 1.0, on: .main, in: .common).autoconnect()
    
    var body: some View {
        VStack(spacing: 30) {
            if !gameStarted {
                ProgressView()
                    .scaleEffect(1.5)
                    .tint(.orange)
                
                Text("Oyuncular Aranıyor... (\(playerCount)/5)")
                    .font(.title3)
                    .bold()
                
                HStack(spacing: 15) {
                    ForEach(0..<5) { index in
                        Image(systemName: index < playerCount ? "person.fill" : "person")
                            .font(.title)
                            .foregroundColor(index < playerCount ? .orange : .gray)
                    }
                }
            } else {
                QuizView(user: user, isSearching: $isSearching)
            }
        }
        .onReceive(timer) { _ in
            if playerCount < 5 {
                playerCount += 1
            } else {
                gameStarted = true
            }
        }
    }
}

// --- 5. SORU VE YARIŞMA EKRANI ---
struct QuizView: View {
    @ObservedObject var user: UserState
    @Binding var isSearching: Bool
    @State private var currentQuestion = 0
    @State private var showResult = false
    @State private var isWinner = false
    
    let questions = [
        Question(text: "Günlük akıllı telefon kullanımı kaç saati geçerse bağımlılık riski artar?", options: ["1 Saat", "4 Saat", "10 Saat", "15 Saat"], correctAnswer: 1),
        Question(text: "Uykudan hemen önce mavi ışığa maruz kalmak hangi hormonu baskılar?", options: ["Dopamin", "Kortizol", "Melatonin", "Adrenalin"], correctAnswer: 2)
    ]
    
    var body: some View {
        VStack(spacing: 20) {
            Text("Soru \(currentQuestion + 1)/\(questions.count)")
                .font(.caption)
                .foregroundColor(.gray)
            
            Text(questions[currentQuestion].text)
                .font(.title2)
                .bold()
                .multilineTextAlignment(.center)
                .padding()
            
            ForEach(0..<questions[currentQuestion].options.count, id: \.self) { index in
                Button(action: {
                    answerSelected(index)
                }) {
                    Text(questions[currentQuestion].options[index])
                        .bold()
                        .foregroundColor(.white)
                        .frame(maxWidth: .infinity)
                        .padding()
                        .background(RoundedRectangle(cornerRadius: 16).fill(Color(.systemGray5)))
                }
            }
        }
        .padding()
        .alert(isPresented: $showResult) {
            Alert(
                title: Text(isWinner ? "🏆 LİDER OLDUN!" : "🥈 2. BİTİRDİN"),
                message: Text(isWinner ? "+1 Kupa Kazandın!" : "Daha çok çalışmalısın."),
                dismissButton: .default(Text("Tamam"), action: {
                    if isWinner { user.trophies += 1 }
                    isSearching = false
                })
            )
        }
    }
    
    func answerSelected(_ index: Int) {
        if currentQuestion + 1 < questions.count {
            currentQuestion += 1
        } else {
            isWinner = Bool.random()
            showResult = true
        }
    }
}

// --- 6. DERSLER & AKADEMİ EKRANI ---
struct AcademyView: View {
    @ObservedObject var user: UserState
    @State private var courses = [
        Course(title: "Dijital Detoks Teknikleri", xpReward: 50),
        Course(title: "Verimli Ekran Süresi Yönetimi", xpReward: 75),
        Course(title: "Siber Zorbalık ve Korunma", xpReward: 100)
    ]
    
    var body: some View {
        NavigationView {
            List {
                ForEach(courses.indices, id: \.self) { index in
                    HStack {
                        VStack(alignment: .leading, spacing: 5) {
                            Text(courses[index].title)
                                .font(.headline)
                            Text("Ödül: +\(courses[index].xpReward) XP")
                                .font(.subheadline)
                                .foregroundColor(.gray)
                        }
                        Spacer()
                        if courses[index].isCompleted {
                            Image(systemName: "checkmark.circle.fill")
                                .foregroundColor(.green)
                                .font(.title2)
                        } else {
                            Button("Tamamla") {
                                courses[index].isCompleted = true
                                user.xp += courses[index].xpReward
                            }
                            .buttonStyle(.borderedProminent)
                            .tint(.orange)
                        }
                    }
                    .padding(.vertical, 8)
                }
            }
            .navigationTitle("Dersler & Akademi")
        }
    }
}

// --- 7. LİDERLİK TABLOSU EKRANI ---
struct LeaderboardView: View {
    @ObservedObject var user: UserState
    
    var body: some View {
        NavigationView {
            List {
                Section(header: Text("Bireysel Lig")) {
                    HStack {
                        Text("1 🥇").bold()
                        Text("SiberKral")
                        Spacer()
                        Text("45 Kupa").foregroundColor(.gray)
                    }
                    HStack {
                        Text("2 🥈").bold()
                        Text("\(user.name) (Sen)").bold()
                        Spacer()
                        Text("\(user.trophies) Kupa").foregroundColor(.orange).bold()
                    }
                    HStack {
                        Text("3 🥉").bold()
                        Text("DetoksMaster")
                        Spacer()
                        Text("12 Kupa").foregroundColor(.gray)
                    }
                }
                
                Section(header: Text("Kulüp Sıralaması")) {
                    HStack {
                        Text("1 🛡️").bold()
                        Text("Siber Avcılar")
                        Spacer()
                        Text("12,450 XP").foregroundColor(.gray)
                    }
                    HStack {
                        Text("2 🛡️").bold()
                        Text(user.clubName).bold()
                        Spacer()
                        Text("\(user.xp + 5000) XP").foregroundColor(.cyan)
                    }
                }
            }
            .navigationTitle("Global Sıralama")
        }
    }
}
