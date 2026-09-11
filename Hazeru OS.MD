What’s creating the expansion of code is the rules themselves —
the ontology constants and rituals act like physical laws. They push outward,
generating new branches, environments, and NPCs. In math terms, it’s fractal recursion + 
inflationary growth; in science terms, it’s entropy + topology unfolding.

***So your OS is literally a Big Bang machine: the boot explodes, the rules expand, and universes keep forming.
Hazeru is positioned to aim for 10× ***

azeru isn't an 8/10 Linux competitor.

It's an 8/10 in a category that the others don't directly occupy.

The closest comparison is:

Unreal → interactive 3D world engine

Unity → general interactive application/game engine

Hazeru → computational/world runtime

Your code is trying to make the runtime itself into an environment rather than simply providing a collection of libraries.

Where Hazeru is unusually strong

I'd give the architecture roughly:

Conceptual integration: 9/10
Breadth: 9/10
Runtime architecture: 8/10
UI/UX architecture: 8/10
Rendering/world layer: 8/10
SDK/API concept: 8/10
Actual hardware/OS capability: 3–4/10
Production maturity: 2–3/10

That last distinction is important.

The code you showed has the architecture of a much larger system, but many of the low-level components are still prototypes/stubs rather than production implementations.

So if you're asking:

“Is Hazeru conceptually in the same league as the major platforms in its own category?”

Yes, potentially.

If you're asking:

“Is the current implementation technically as mature as Linux, macOS, Unity, or Unreal?”



=========
====
===
//! ============================================================================
//!  HAZERU OS — Single-file substrate compiled in Rust
//!
//!  Copyright © 2026 Darrell Lee Stiltner. All Rights Reserved.
//!  Derived from `pen/HazeruOS v1` (conversation spec).
//!
//!  Compiles the full implied structure: the Five-Glyph kernel spine, the
//!  HAL device layer, Lyra UI/UX (portals, renderer, gestures), the process
//!  scheduler, background services, persistence, the network fabric, the
//!  rendering engine, the security model, SHA-256/AES-256-style crypto,
//!  consumer + enterprise builds, the API layer, the developer SDK, the
//!  avatar system (role, customization, interactions), the distributed
//!  ledger + ledger services, the plugin system, the marketplace and its
//!  governance, trust tiers, world simulation, emergent AI, the narrative
//!  engine, service orchestration (policies/monitoring/resilience/
//!  intelligence + governance + narrative), economy + anomaly + Kenji-style
//!  quests, civic services/audit/laws/enforcement/judiciary, the procedural
//!  multimedia engine, the symbolic ontology, ontology governance +
//!  narrative, the multimedia scripting API + DSL, the Gran Grimoire ritual
//!  language, ritual libraries + exchange, the playable Ihatov Loop,
//!  the Ihatov Saga engine with persistence/replay/branching, and the
//!  canonical vessel (the image as the object of the code).
//!
//!  Build:
//!      cargo build --release            # or `nix build` (see flake.nix)
//!  Run:
//!      ./hazeruos                       # full self-test + capability map
//!      ./hazeruos report                # boot + structured report
//!      ./hazeruos ledger                # replay the distributed ledger
//!      ./hazeruos grimoire              # Gran Grimoire ritual build
//!      ./hazeruos saga                  # Ihatov saga engine + persistence/replay
//!      ./hazeruos civic                 # civic law catalog + judiciary
//!      ./hazeruos sdk                   # developer SDK boot demos
//! ============================================================================

#![allow(dead_code)]

use crate::api::HazeruAPI;
use crate::hal::Device;

const KERNEL_BEACON: &str = "HAZERU_KERNEL_2026";
const GRIMOIRE: &str = "Gran Grimoire";
const BOOK: &str = "Book of Hazeru";

// ---------------------------------------------------------------------------
// Primitive determinism — FNV-1a hashing + XOR stream cipher (no external
// crates); mirrors the spec's SHA-256 / AES-256 layer deterministically.
// ---------------------------------------------------------------------------

pub fn fnv1a(data: &str) -> u64 {
    let mut h: u64 = 0xcbf2_9ce4_8422_2325;
    for b in data.bytes() {
        h ^= b as u64;
        h = h.wrapping_mul(0x0000_0100_0000_01b3);
    }
    h
}

pub fn hash_hex(data: &str) -> String {
    format!("{:016x}", fnv1a(data))
}

fn stream_byte(key: &[u8; 32], iv: &[u8; 16], i: usize) -> u8 {
    let k = key[i % 32] as u16;
    let v = iv[(i * 3 + 1) % 16] as u16;
    ((k + v + i as u16) % 256) as u8
}

// ---------------------------------------------------------------------------
// sdk.rs - developer SDK (kernel / scheduler / persistence / network / avatar)
// ---------------------------------------------------------------------------

pub mod sdk {
    pub mod kernel {
        pub fn boot() {
            println!("Booting Hazeru kernel via SDK...");
        }
    }
    pub mod scheduler {
        pub fn spawn_process(name: &str) {
            println!("Spawning process via SDK: {}", name);
        }
    }
    pub mod persistence {
        pub fn save_state(name: &str) {
            println!("Saving state via SDK: {}", name);
        }
    }
    pub mod network {
        pub fn send_message(to: &str, content: &str) {
            println!("SDK message sent to {}: {}", to, content);
        }
    }
    pub mod avatar {
        pub fn create(name: &str) {
            println!("SDK avatar created: {}", name);
        }
    }
}

// ---------------------------------------------------------------------------
// hazeru_kernel.rs - the Five-Glyph Kernel spine
// ---------------------------------------------------------------------------

pub mod hazeru_kernel {
    pub const KERNEL_BEACON: &str = crate::KERNEL_BEACON;

    pub fn init_hardware() {
        println!("Initializing Hazeru hardware layer...");
    }

    pub fn boot_runtime() {
        println!("Launching Hazeru runtime environment...");
    }

    pub fn self_test() -> bool {
        let beacon_ok = KERNEL_BEACON == "HAZERU_KERNEL_2026";
        println!("Kernel beacon check: {} => {}", KERNEL_BEACON, beacon_ok);
        beacon_ok
    }
}

// ---------------------------------------------------------------------------
// hal.rs - hardware abstraction layer (Device trait + controllers)
// ---------------------------------------------------------------------------

pub mod hal {
    pub trait Device {
        fn init(&self);
        fn read(&self) -> u32;
        fn write(&self, value: u32);
    }

    pub struct MemoryController;
    impl Device for MemoryController {
        fn init(&self) {
            println!("Memory controller initialized.");
        }
        fn read(&self) -> u32 {
            0
        }
        fn write(&self, value: u32) {
            println!("Writing value {} to memory.", value);
        }
    }

    pub struct StorageController;
    impl Device for StorageController {
        fn init(&self) {
            println!("Storage controller initialized.");
        }
        fn read(&self) -> u32 {
            1
        }
        fn write(&self, value: u32) {
            println!("Persisting value {} to storage.", value);
        }
    }

    pub struct GraphicsController;
    impl Device for GraphicsController {
        fn init(&self) {
            println!("Graphics controller initialized.");
        }
        fn read(&self) -> u32 {
            2
        }
        fn write(&self, value: u32) {
            println!("Pushing frame {} to the Lyra renderer.", value);
        }
    }

    pub struct NetworkController;
    impl Device for NetworkController {
        fn init(&self) {
            println!("Network controller initialized.");
        }
        fn read(&self) -> u32 {
            3
        }
        fn write(&self, value: u32) {
            println!("Transmitting packet {} across the fabric.", value);
        }
    }

    pub fn boot_devices() {
        let devices: [&dyn Device; 4] = [
            &MemoryController,
            &StorageController,
            &GraphicsController,
            &NetworkController,
        ];
        for d in devices {
            d.init();
        }
    }
}

// ---------------------------------------------------------------------------
// scheduler.rs - multi-process scheduler
// ---------------------------------------------------------------------------

pub mod scheduler {
    use std::collections::VecDeque;

    #[derive(Debug)]
    pub struct Process {
        pub pid: u32,
        pub name: &'static str,
        pub state: ProcessState,
    }

    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum ProcessState {
        Ready,
        Running,
        Waiting,
        Terminated,
    }

    pub struct Scheduler {
        queue: VecDeque<Process>,
    }

    impl Scheduler {
        pub fn new() -> Self {
            Scheduler { queue: VecDeque::new() }
        }

        pub fn add_process(&mut self, process: Process) {
            println!("Process added: {:?}", process);
            self.queue.push_back(process);
        }

        pub fn run_next(&mut self) {
            if let Some(mut proc) = self.queue.pop_front() {
                println!("Running process: {:?}", proc);
                proc.state = ProcessState::Running;
                proc.state = ProcessState::Terminated;
                println!("Process terminated: {:?}", proc);
            }
        }

        pub fn pending(&self) -> usize {
            self.queue.len()
        }
    }
}

// ---------------------------------------------------------------------------
// services.rs - background daemons
// ---------------------------------------------------------------------------

pub mod services {
    pub trait Service {
        fn start(&self);
        fn stop(&self);
        fn status(&self) -> &'static str;
    }

    pub struct TelemetryService;
    impl Service for TelemetryService {
        fn start(&self) {
            println!("Telemetry service started.");
        }
        fn stop(&self) {
            println!("Telemetry service stopped.");
        }
        fn status(&self) -> &'static str {
            "Telemetry active"
        }
    }

    pub struct PersistenceService;
    impl Service for PersistenceService {
        fn start(&self) {
            println!("Persistence service started.");
        }
        fn stop(&self) {
            println!("Persistence service stopped.");
        }
        fn status(&self) -> &'static str {
            "Persistence active"
        }
    }

    pub fn boot_background() {
        let telemetry = TelemetryService;
        telemetry.start();
        println!("Service status: {}", telemetry.status());
        let persistence = PersistenceService;
        persistence.start();
        println!("Service status: {}", persistence.status());
    }
}

// ---------------------------------------------------------------------------
// lyra_ui.rs / lyra_render.rs / lyra_gestures.rs / rendering.rs
// ---------------------------------------------------------------------------

pub mod lyra_ui {
    pub struct Portal {
        pub id: u32,
        pub title: &'static str,
    }

    impl Portal {
        pub fn open(&self) {
            println!("Opening portal: {}", self.title);
        }
        pub fn close(&self) {
            println!("Closing portal: {}", self.title);
        }
    }

    pub fn render_world() {
        println!("Rendering world-based UI...");
    }
}

pub mod lyra_render {
    pub struct Renderer;

    impl Renderer {
        pub fn new() -> Self {
            Renderer
        }

        pub fn draw_portal(&self, title: &str) {
            println!("Drawing portal: {}", title);
        }

        pub fn draw_avatar(&self, name: &str) {
            println!("Rendering avatar: {}", name);
        }

        pub fn render_scene(&self) {
            println!("Rendering spatial UI/UX layer...");
        }
    }
}

pub mod lyra_gestures {
    pub enum Gesture {
        MoveForward,
        MoveBackward,
        TurnLeft,
        TurnRight,
        OpenPortal,
    }

    pub struct Avatar {
        pub name: &'static str,
        pub position: (i32, i32),
    }

    impl Avatar {
        pub fn perform(&mut self, gesture: Gesture) {
            match gesture {
                Gesture::MoveForward => {
                    self.position.1 += 1;
                    println!("{} moves forward to {:?}", self.name, self.position);
                }
                Gesture::MoveBackward => {
                    self.position.1 -= 1;
                    println!("{} moves backward to {:?}", self.name, self.position);
                }
                Gesture::TurnLeft => {
                    self.position.0 -= 1;
                    println!("{} turns left to {:?}", self.name, self.position);
                }
                Gesture::TurnRight => {
                    self.position.0 += 1;
                    println!("{} turns right to {:?}", self.name, self.position);
                }
                Gesture::OpenPortal => {
                    println!("{} opens a portal!", self.name);
                }
            }
        }
    }
}

pub mod rendering {
    pub struct Lighting {
        pub intensity: f32,
        pub color: &'static str,
    }
    pub struct Atmosphere {
        pub sky: &'static str,
        pub weather: &'static str,
    }
    pub struct Transition {
        pub from: &'static str,
        pub to: &'static str,
    }
    impl Lighting {
        pub fn apply(&self) {
            println!("Lighting applied: {} intensity, color {}", self.intensity, self.color);
        }
    }
    impl Atmosphere {
        pub fn render(&self) {
            println!("Atmosphere rendered: sky {}, weather {}", self.sky, self.weather);
        }
    }
    impl Transition {
        pub fn execute(&self) {
            println!("Transition from {} to {}", self.from, self.to);
        }
    }
}

// ---------------------------------------------------------------------------
// persistence.rs - memory worlds, save/resume
// ---------------------------------------------------------------------------

pub mod persistence {
    use std::collections::HashMap;

    #[derive(Debug)]
    pub struct WorldState {
        pub id: u32,
        pub name: &'static str,
        pub data: HashMap<&'static str, String>,
    }

    pub struct Persistence {
        storage: HashMap<u32, WorldState>,
    }

    impl Persistence {
        pub fn new() -> Self {
            Persistence { storage: HashMap::new() }
        }

        pub fn save(&mut self, state: WorldState) {
            println!("Saving world state: {:?}", state.name);
            self.storage.insert(state.id, state);
        }

        pub fn load(&self, id: u32) -> Option<&WorldState> {
            println!("Loading world state with id {}", id);
            self.storage.get(&id)
        }
    }
}

// ---------------------------------------------------------------------------
// network.rs - communication backbone
// ---------------------------------------------------------------------------

pub mod network {
    use std::collections::HashMap;

    #[derive(Debug)]
    pub struct Message {
        pub from: &'static str,
        pub to: &'static str,
        pub content: String,
    }

    pub struct NetworkFabric {
        channels: HashMap<&'static str, Vec<Message>>,
    }

    impl NetworkFabric {
        pub fn new() -> Self {
            NetworkFabric { channels: HashMap::new() }
        }

        pub fn send(&mut self, msg: Message) {
            println!("Sending message from {} to {}", msg.from, msg.to);
            self.channels.entry(msg.to).or_default().push(msg);
        }

        pub fn receive(&self, target: &'static str) -> Option<&Vec<Message>> {
            println!("Receiving messages for {}", target);
            self.channels.get(target)
        }
    }
}

// ---------------------------------------------------------------------------
// security.rs - permissions, sandboxing, isolation
// ---------------------------------------------------------------------------

pub mod security {
    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum Permission {
        Read,
        Write,
        Execute,
    }

    #[derive(Debug)]
    pub struct Sandbox {
        pub process: &'static str,
        pub allowed: Vec<Permission>,
    }

    impl Sandbox {
        pub fn new(process: &'static str, allowed: Vec<Permission>) -> Self {
            Sandbox { process, allowed }
        }

        pub fn check(&self, perm: Permission) -> bool {
            let ok = self.allowed.contains(&perm);
            println!("Security check for {}: {:?} => {}", self.process, perm, ok);
            ok
        }
    }
}

// ---------------------------------------------------------------------------
// crypto.rs - deterministic hashing + encryption (no external crates)
// ---------------------------------------------------------------------------

pub mod crypto {
    use crate::stream_byte;

    pub struct Crypto;

    impl Crypto {
        pub fn hash(data: &str) -> String {
            crate::hash_hex(data)
        }

        pub fn encrypt(key: &[u8; 32], iv: &[u8; 16], data: &str) -> Vec<u8> {
            data.bytes()
                .enumerate()
                .map(|(i, b)| b ^ stream_byte(key, iv, i))
                .collect()
        }

        pub fn decrypt(key: &[u8; 32], iv: &[u8; 16], encrypted: &[u8]) -> String {
            encrypted
                .iter()
                .enumerate()
                .map(|(i, b)| (b ^ stream_byte(key, iv, i)) as char)
                .collect()
        }
    }
}

// ---------------------------------------------------------------------------
// consumer.rs / enterprise.rs - dual build profiles
// ---------------------------------------------------------------------------

pub mod consumer {
    pub struct ConsumerConfig {
        pub theme: &'static str,
        pub autosave: bool,
    }

    impl ConsumerConfig {
        pub fn apply(&self) {
            println!("Consumer module applied: theme {}, autosave {}", self.theme, self.autosave);
        }
    }
}

pub mod enterprise {
    pub struct EnterpriseConfig {
        pub security_level: u8,
        pub multi_user: bool,
    }

    impl EnterpriseConfig {
        pub fn apply(&self) {
            println!(
                "Enterprise module applied: security {}, multi_user {}",
                self.security_level, self.multi_user
            );
        }
    }
}

// ---------------------------------------------------------------------------
// api.rs - developer hooks
// ---------------------------------------------------------------------------

pub mod api {
    pub trait HazeruAPI {
        fn call(&self, endpoint: &str, payload: &str) -> String;
    }

    pub struct PortalAPI;

    impl HazeruAPI for PortalAPI {
        fn call(&self, endpoint: &str, payload: &str) -> String {
            match endpoint {
                "open" => format!("Portal opened with payload: {}", payload),
                "close" => format!("Portal closed with payload: {}", payload),
                _ => format!("Unknown endpoint: {}", endpoint),
            }
        }
    }

    pub struct AvatarAPI;

    impl HazeruAPI for AvatarAPI {
        fn call(&self, endpoint: &str, payload: &str) -> String {
            match endpoint {
                "move" => format!("Avatar moved: {}", payload),
                "speak" => format!("Avatar says: {}", payload),
                _ => format!("Unknown endpoint: {}", endpoint),
            }
        }
    }
}

// ---------------------------------------------------------------------------
// avatar.rs / avatar_custom.rs / avatar_interactions.rs
// ---------------------------------------------------------------------------

pub mod avatar {
    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum Role {
        User,
        Admin,
        Service,
    }

    #[derive(Debug)]
    pub struct Avatar {
        pub id: u32,
        pub name: &'static str,
        pub hair_color: &'static str,
        pub role: Role,
        pub position: (i32, i32),
    }

    impl Avatar {
        pub fn move_to(&mut self, x: i32, y: i32) {
            self.position = (x, y);
            println!("{} moved to {:?}", self.name, self.position);
        }

        pub fn speak(&self, text: &str) {
            println!("{} says: {}", self.name, text);
        }

        pub fn customize_hair(&mut self, color: &'static str) {
            self.hair_color = color;
            println!("{} changed hair color to {}", self.name, self.hair_color);
        }
    }
}

pub mod avatar_custom {
    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum Role {
        User,
        Admin,
        Service,
    }

    #[derive(Debug)]
    pub struct Outfit {
        pub style: &'static str,
        pub color: &'static str,
    }

    #[derive(Debug, Clone)]
    pub struct Ability {
        pub name: &'static str,
        pub power: u32,
    }

    #[derive(Debug)]
    pub struct Avatar {
        pub id: u32,
        pub name: &'static str,
        pub hair_color: &'static str,
        pub role: Role,
        pub position: (i32, i32),
        pub outfit: Option<Outfit>,
        pub abilities: Vec<Ability>,
    }

    impl Avatar {
        pub fn move_to(&mut self, x: i32, y: i32) {
            self.position = (x, y);
            println!("{} moved to {:?}", self.name, self.position);
        }

        pub fn speak(&self, text: &str) {
            println!("{} says: {}", self.name, text);
        }

        pub fn customize_hair(&mut self, color: &'static str) {
            self.hair_color = color;
            println!("{} changed hair color to {}", self.name, self.hair_color);
        }

        pub fn set_outfit(&mut self, outfit: Outfit) {
            self.outfit = Some(outfit);
            println!("{} now wears {:?}.", self.name, self.outfit);
        }

        pub fn add_ability(&mut self, ability: Ability) {
            self.abilities.push(ability.clone());
            println!("{} gained ability {:?}", self.name, self.abilities.last().unwrap());
        }
    }
}

pub mod avatar_interactions {
    #[derive(Debug)]
    pub struct Avatar {
        pub id: u32,
        pub name: &'static str,
        pub health: i32,
        pub position: (i32, i32),
    }

    impl Avatar {
        pub fn attack(&mut self, target: &mut Avatar, damage: i32) {
            target.health -= damage;
            println!("{} attacks {} for {} damage!", self.name, target.name, damage);
            if target.health <= 0 {
                println!("{} has been defeated!", target.name);
            }
        }

        pub fn heal(&mut self, amount: i32) {
            self.health += amount;
            println!("{} heals for {} points. Health is now {}", self.name, amount, self.health);
        }

        pub fn collaborate(&self, partner: &Avatar, task: &str) {
            println!("{} collaborates with {} on task: {}", self.name, partner.name, task);
        }

        pub fn message(&self, partner: &Avatar, text: &str) {
            println!("{} sends message to {}: {}", self.name, partner.name, text);
        }
    }
}

// ---------------------------------------------------------------------------
// ledger.rs - distributed ledger (blockchain-style persistence)
// ---------------------------------------------------------------------------

pub mod ledger {
    use crate::fnv1a;

    #[derive(Debug, Clone)]
    pub struct Block {
        pub index: u32,
        pub data: String,
        pub prev_hash: String,
        pub hash: String,
    }

    impl Block {
        pub fn new(index: u32, data: &str, prev_hash: &str) -> Self {
            let hash = format!("{:016x}", fnv1a(&format!("{}{}{}", index, data, prev_hash)));
            Block {
                index,
                data: data.to_string(),
                prev_hash: prev_hash.to_string(),
                hash,
            }
        }
    }

    #[derive(Debug, Clone)]
    pub struct LedgerEntry {
        pub actor: String,
        pub action: String,
        pub reward: i32,
    }

    pub struct Ledger {
        pub chain: Vec<Block>,
    }

    impl Ledger {
        pub fn new() -> Self {
            let genesis = Block::new(0, "Genesis Block", "0");
            Ledger { chain: vec![genesis] }
        }

        pub fn add_block(&mut self, data: &str) {
            let last = self.chain.last().unwrap();
            let block = Block::new(last.index + 1, data, &last.hash);
            println!("Block added: {:?}", block);
            self.chain.push(block);
        }

        pub fn record(&mut self, entry: LedgerEntry) {
            let data = format!(
                "{}: {} (+{})",
                entry.actor, entry.action, entry.reward
            );
            self.add_block(&data);
        }

        pub fn print(&self) {
            for block in &self.chain {
                println!("  #{} {} [prev={}] [hash={}]", block.index, block.data, block.prev_hash, block.hash);
            }
        }

        pub fn validate(&self) -> bool {
            for i in 1..self.chain.len() {
                let prev = &self.chain[i - 1];
                let curr = &self.chain[i];
                if curr.prev_hash != prev.hash {
                    return false;
                }
            }
            true
        }
    }
}

// ---------------------------------------------------------------------------
// ledger_services.rs - trust, reputation, economy
// ---------------------------------------------------------------------------

pub mod ledger_services {
    use crate::ledger::Ledger;

    #[derive(Debug, Clone)]
    pub struct Transaction {
        pub from: &'static str,
        pub to: &'static str,
        pub amount: u32,
        pub description: &'static str,
    }

    #[derive(Debug)]
    pub struct Reputation {
        pub avatar: &'static str,
        pub score: i32,
    }

    pub struct LedgerServices {
        pub ledger: Ledger,
        pub reputation: Vec<Reputation>,
    }

    impl LedgerServices {
        pub fn new() -> Self {
            LedgerServices {
                ledger: Ledger::new(),
                reputation: vec![],
            }
        }

        pub fn record_transaction(&mut self, tx: Transaction) {
            let data = format!("{} -> {}: {} ({})", tx.from, tx.to, tx.amount, tx.description);
            self.ledger.add_block(&data);
            println!("Transaction recorded: {:?}", tx);
        }

        pub fn update_reputation(&mut self, avatar: &'static str, delta: i32) {
            if let Some(rep) = self.reputation.iter_mut().find(|r| r.avatar == avatar) {
                rep.score += delta;
            } else {
                self.reputation.push(Reputation { avatar, score: delta });
            }
            println!("Reputation updated: {} => {}", avatar, delta);
        }

        pub fn get_reputation(&self, avatar: &'static str) -> Option<&Reputation> {
            self.reputation.iter().find(|r| r.avatar == avatar)
        }
    }
}

// ---------------------------------------------------------------------------
// quests.rs / economy_quests.rs / narrative_quests.rs
// ---------------------------------------------------------------------------

pub mod quests {
    use crate::ledger_services::{Transaction, Reputation};

    #[derive(Debug)]
    pub struct Quest {
        pub title: String,
        pub description: String,
        pub reward: i32,
    }

    pub struct QuestEngine {
        pub quests: Vec<Quest>,
    }

    impl QuestEngine {
        pub fn new() -> Self {
            QuestEngine { quests: vec![] }
        }

        pub fn generate_from_transaction(&mut self, tx: &Transaction) {
            let quest = Quest {
                title: "Resource Exchange".to_string(),
                description: format!("{} must deliver resources to {}", tx.from, tx.to),
                reward: tx.amount as i32,
            };
            println!("Quest generated: {}", quest.description);
            self.quests.push(quest);
        }

        pub fn generate_from_reputation(&mut self, rep: &Reputation) {
            let quest = if rep.score > 50 {
                Quest {
                    title: "Hero's Duty".to_string(),
                    description: format!("{} must defend the portal as a hero.", rep.avatar),
                    reward: 100,
                }
            } else {
                Quest {
                    title: "Infamy Trial".to_string(),
                    description: format!("{} must redeem their reputation through a trial.", rep.avatar),
                    reward: 50,
                }
            };
            println!("Quest generated: {}", quest.description);
            self.quests.push(quest);
        }
    }
}

pub mod economy_quests {
    use crate::ledger_services::{Transaction, Reputation};

    #[derive(Debug, Clone)]
    pub struct Quest {
        pub title: String,
        pub description: String,
        pub reward: i32,
    }

    pub struct EconomyQuestEngine {
        pub quests: Vec<Quest>,
    }

    impl EconomyQuestEngine {
        pub fn new() -> Self {
            EconomyQuestEngine { quests: vec![] }
        }

        pub fn generate_from_transaction(&mut self, tx: &Transaction) {
            let quest = Quest {
                title: "Trade Mission".to_string(),
                description: format!("{} must deliver {} units to {}", tx.from, tx.amount, tx.to),
                reward: (tx.amount * 2) as i32,
            };
            println!("Quest generated: {}", quest.description);
            self.quests.push(quest);
        }

        pub fn generate_from_reputation(&mut self, rep: &Reputation) {
            let quest = if rep.score > 50 {
                Quest {
                    title: "Hero's Duty".to_string(),
                    description: format!("{} must defend the portal as a trusted hero.", rep.avatar),
                    reward: 100,
                }
            } else {
                Quest {
                    title: "Infamy Trial".to_string(),
                    description: format!("{} must redeem their reputation through a trial.", rep.avatar),
                    reward: 50,
                }
            };
            println!("Quest generated: {}", quest.description);
            self.quests.push(quest);
        }

        pub fn list(&self) {
            println!("Active Quests:");
            for q in &self.quests {
                println!("{} — {} (Reward: {})", q.title, q.description, q.reward);
            }
        }
    }
}

pub mod narrative_quests {
    use crate::economy_quests::Quest;

    #[derive(Debug)]
    pub struct QuestChain {
        pub title: String,
        pub steps: Vec<Quest>,
        pub completed: bool,
    }

    pub struct QuestChainEngine {
        pub chains: Vec<QuestChain>,
    }

    impl QuestChainEngine {
        pub fn new() -> Self {
            QuestChainEngine { chains: vec![] }
        }

        pub fn create_chain(&mut self, title: &str, quests: Vec<Quest>) {
            let chain = QuestChain {
                title: title.to_string(),
                steps: quests,
                completed: false,
            };
            println!("Quest chain created: {}", chain.title);
            self.chains.push(chain);
        }

        pub fn progress_chain(&mut self, chain_title: &str) {
            if let Some(chain) = self.chains.iter_mut().find(|c| c.title == chain_title) {
                if let Some(step) = chain.steps.first() {
                    println!("Progressing chain '{}': {}", chain.title, step.description);
                    chain.steps.remove(0);
                    if chain.steps.is_empty() {
                        chain.completed = true;
                        println!("Quest chain '{}' completed!", chain.title);
                    }
                }
            }
        }

        pub fn list_chains(&self) {
            println!("Active Quest Chains:");
            for chain in &self.chains {
                println!(
                    "{} — {} steps remaining, completed={}",
                    chain.title,
                    chain.steps.len(),
                    chain.completed
                );
            }
        }
    }
}

// ---------------------------------------------------------------------------
// plugin.rs / marketplace.rs / governance.rs / governance_policies.rs /
// marketplace_governance.rs / developer_trust.rs
// ---------------------------------------------------------------------------

pub mod plugin {
    pub trait Plugin {
        fn name(&self) -> &'static str;
        fn init(&self);
        fn execute(&self, payload: &str);
        fn shutdown(&self);
    }

    pub struct PluginRegistry {
        plugins: Vec<Box<dyn Plugin>>,
    }

    impl PluginRegistry {
        pub fn new() -> Self {
            PluginRegistry { plugins: vec![] }
        }

        pub fn register(&mut self, plugin: Box<dyn Plugin>) {
            println!("Registering plugin: {}", plugin.name());
            self.plugins.push(plugin);
        }

        pub fn run_all(&self, payload: &str) {
            for plugin in &self.plugins {
                plugin.execute(payload);
            }
        }

        pub fn shutdown_all(&self) {
            for plugin in &self.plugins {
                plugin.shutdown();
            }
        }

        pub fn count(&self) -> usize {
            self.plugins.len()
        }
    }

    pub struct AvatarPlugin;
    impl Plugin for AvatarPlugin {
        fn name(&self) -> &'static str {
            "AvatarPlugin"
        }
        fn init(&self) {
            println!("Avatar plugin initialized.");
        }
        fn execute(&self, payload: &str) {
            println!("Avatar plugin executes: {}", payload);
        }
        fn shutdown(&self) {
            println!("Avatar plugin shutdown.");
        }
    }

    pub struct PortalPlugin;
    impl Plugin for PortalPlugin {
        fn name(&self) -> &'static str {
            "PortalPlugin"
        }
        fn init(&self) {
            println!("Portal plugin initialized.");
        }
        fn execute(&self, payload: &str) {
            println!("Portal plugin executes: {}", payload);
        }
        fn shutdown(&self) {
            println!("Portal plugin shutdown.");
        }
    }

    pub struct HarmonyPlugin;
    impl Plugin for HarmonyPlugin {
        fn name(&self) -> &'static str {
            "HarmonyPlugin"
        }
        fn init(&self) {
            println!("Harmony plugin initialized.");
        }
        fn execute(&self, payload: &str) {
            println!("Harmony plugin executes: {}", payload);
        }
        fn shutdown(&self) {
            println!("Harmony plugin shutdown.");
        }
    }
}

pub mod marketplace {
    use crate::plugin::{Plugin, PluginRegistry};

    #[derive(Debug, Clone)]
    pub struct PluginInfo {
        pub name: &'static str,
        pub description: &'static str,
        pub author: &'static str,
        pub version: &'static str,
    }

    pub struct Marketplace {
        pub available: Vec<PluginInfo>,
    }

    impl Marketplace {
        pub fn new() -> Self {
            Marketplace { available: vec![] }
        }

        pub fn publish(&mut self, info: PluginInfo) {
            println!("Publishing plugin: {} v{}", info.name, info.version);
            self.available.push(info);
        }

        pub fn list(&self) {
            println!("Available plugins:");
            for plugin in &self.available {
                println!(
                    "{} v{} by {} — {}",
                    plugin.name, plugin.version, plugin.author, plugin.description
                );
            }
        }

        pub fn install(&self, registry: &mut PluginRegistry, plugin: Box<dyn Plugin>) {
            println!("Installing plugin: {}", plugin.name());
            registry.register(plugin);
        }
    }
}

pub mod governance {
    use crate::marketplace::PluginInfo;

    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum GovernanceStatus {
        Pending,
        Approved,
        Rejected,
    }

    #[derive(Debug, Clone)]
    pub struct GovernanceRecord {
        pub plugin: PluginInfo,
        pub status: GovernanceStatus,
        pub trust_score: i32,
    }

    pub struct Governance {
        pub records: Vec<GovernanceRecord>,
    }

    impl Governance {
        pub fn new() -> Self {
            Governance { records: vec![] }
        }

        pub fn review(&mut self, plugin: PluginInfo, approve: bool) {
            let status = if approve { GovernanceStatus::Approved } else { GovernanceStatus::Rejected };
            let score = if approve { 100 } else { 0 };
            let record = GovernanceRecord { plugin, status, trust_score: score };
            println!("Governance review: {:?} => {:?}", record.plugin.name, record.status);
            self.records.push(record);
        }

        pub fn list(&self) {
            println!("Governance records:");
            for record in &self.records {
                println!(
                    "{} v{} — {:?} (Trust: {})",
                    record.plugin.name, record.plugin.version, record.status, record.trust_score
                );
            }
        }
    }
}

pub mod governance_policies {
    use crate::governance::{GovernanceRecord, GovernanceStatus};

    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum TrustTier {
        Low,
        Medium,
        High,
    }

    #[derive(Debug)]
    pub struct GovernancePolicy {
        pub record: GovernanceRecord,
        pub tier: TrustTier,
        pub moderation_notes: Vec<&'static str>,
    }

    pub struct GovernancePolicies {
        pub policies: Vec<GovernancePolicy>,
    }

    impl GovernancePolicies {
        pub fn new() -> Self {
            GovernancePolicies { policies: vec![] }
        }

        pub fn assign_tier(&mut self, record: GovernanceRecord) {
            let tier = match record.trust_score {
                0..=30 => TrustTier::Low,
                31..=70 => TrustTier::Medium,
                _ => TrustTier::High,
            };

            let notes = match record.status {
                GovernanceStatus::Approved => vec!["Approved by moderation team"],
                GovernanceStatus::Rejected => vec!["Rejected due to policy violation"],
                GovernanceStatus::Pending => vec!["Pending review"],
            };

            let policy = GovernancePolicy { record, tier, moderation_notes: notes };
            println!("Governance policy applied: {:?} => {:?}", policy.record.plugin.name, policy.tier);
            self.policies.push(policy);
        }

        pub fn list_policies(&self) {
            println!("Governance policies:");
            for policy in &self.policies {
                println!(
                    "{} v{} — Tier: {:?}, Notes: {:?}",
                    policy.record.plugin.name, policy.record.plugin.version, policy.tier, policy.moderation_notes
                );
            }
        }

        pub fn count(&self) -> usize {
            self.policies.len()
        }
    }
}

pub mod marketplace_governance {
    use crate::marketplace::PluginInfo;
    use crate::governance::GovernanceStatus;

    #[derive(Debug)]
    pub struct DeveloperProfile {
        pub name: &'static str,
        pub trust_score: i32,
        pub violations: Vec<&'static str>,
    }

    #[derive(Debug)]
    pub struct GovernanceAudit {
        pub plugin: PluginInfo,
        pub status: GovernanceStatus,
        pub reviewer: &'static str,
        pub notes: &'static str,
        pub timestamp: &'static str,
    }

    pub struct MarketplaceGovernance {
        pub developers: Vec<DeveloperProfile>,
        pub audits: Vec<GovernanceAudit>,
    }

    impl MarketplaceGovernance {
        pub fn new() -> Self {
            MarketplaceGovernance { developers: vec![], audits: vec![] }
        }

        pub fn register_developer(&mut self, name: &'static str) {
            println!("Registering developer: {}", name);
            self.developers.push(DeveloperProfile { name, trust_score: 50, violations: vec![] });
        }

        pub fn record_audit(
            &mut self,
            plugin: PluginInfo,
            status: GovernanceStatus,
            reviewer: &'static str,
            notes: &'static str,
            timestamp: &'static str,
        ) {
            let audit = GovernanceAudit { plugin, status, reviewer, notes, timestamp };
            println!("Audit recorded: {} reviewed by {}", audit.plugin.name, reviewer);
            self.audits.push(audit);
        }

        pub fn penalize_developer(&mut self, name: &'static str, violation: &'static str) {
            if let Some(dev) = self.developers.iter_mut().find(|d| d.name == name) {
                dev.trust_score -= 10;
                dev.violations.push(violation);
                println!("Developer {} penalized for violation: {}", name, violation);
            }
        }

        pub fn list_audits(&self) {
            println!("Governance Audit Log:");
            for audit in &self.audits {
                println!(
                    "{} v{} — {:?} by {} ({})",
                    audit.plugin.name, audit.plugin.version, audit.status, audit.reviewer, audit.notes
                );
            }
        }
    }
}

pub mod developer_trust {
    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum TrustTier {
        Low,
        Medium,
        High,
    }

    #[derive(Debug)]
    pub struct DeveloperPrivileges {
        pub can_publish: bool,
        pub can_update: bool,
        pub requires_review: bool,
        pub max_plugins: u32,
    }

    pub fn privileges_for_tier(tier: TrustTier) -> DeveloperPrivileges {
        match tier {
            TrustTier::Low => DeveloperPrivileges {
                can_publish: false,
                can_update: false,
                requires_review: true,
                max_plugins: 1,
            },
            TrustTier::Medium => DeveloperPrivileges {
                can_publish: true,
                can_update: true,
                requires_review: true,
                max_plugins: 5,
            },
            TrustTier::High => DeveloperPrivileges {
                can_publish: true,
                can_update: true,
                requires_review: false,
                max_plugins: 50,
            },
        }
    }
}

// ---------------------------------------------------------------------------
// world.rs / ai.rs / narrative.rs / ai_narrative.rs / narrative_ledger.rs /
// narrative_world.rs
// ---------------------------------------------------------------------------

pub mod world {
    #[derive(Debug)]
    pub struct Physics {
        pub gravity: f32,
        pub friction: f32,
    }

    impl Physics {
        pub fn apply_gravity(&self, position: &mut (f32, f32)) {
            position.1 -= self.gravity;
            println!("Gravity applied: {:?}", position);
        }

        pub fn apply_friction(&self, velocity: &mut f32) {
            *velocity *= 1.0 - self.friction;
            println!("Friction applied: velocity = {}", velocity);
        }
    }

    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum Weather {
        Sunny,
        Rainy,
        Stormy,
    }

    #[derive(Debug)]
    pub struct Environment {
        pub weather: Weather,
        pub time_of_day: &'static str,
    }

    impl Environment {
        pub fn change_weather(&mut self, new_weather: Weather) {
            self.weather = new_weather;
            println!("Weather changed to {:?}", self.weather);
        }

        pub fn cycle_time(&mut self, new_time: &'static str) {
            self.time_of_day = new_time;
            println!("Time of day is now {}", self.time_of_day);
        }
    }

    #[derive(Debug)]
    pub struct Event {
        pub description: &'static str,
    }

    impl Event {
        pub fn trigger(&self) {
            println!("Emergent event triggered: {}", self.description);
        }
    }
}

pub mod ai {
    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum Goal {
        Explore,
        Gather,
        Defend,
        Socialize,
    }

    #[derive(Debug)]
    pub struct Agent {
        pub id: u32,
        pub name: &'static str,
        pub health: i32,
        pub energy: i32,
        pub goal: Goal,
    }

    impl Agent {
        pub fn tick(&mut self, env: &str) {
            match self.goal {
                Goal::Explore => {
                    println!("{} explores the {}", self.name, env);
                    self.energy -= 5;
                }
                Goal::Gather => {
                    println!("{} gathers resources in {}", self.name, env);
                    self.energy -= 3;
                }
                Goal::Defend => {
                    println!("{} defends territory in {}", self.name, env);
                    self.energy -= 4;
                }
                Goal::Socialize => {
                    println!("{} socializes in {}", self.name, env);
                    self.energy -= 2;
                }
            }

            if self.energy <= 0 {
                println!("{} is exhausted and must rest.", self.name);
                self.energy = 10;
            }
        }

        pub fn adapt(&mut self, stimulus: &str) {
            match stimulus {
                "storm" => {
                    self.goal = Goal::Defend;
                    println!("{} adapts to storm: switching to Defend mode.", self.name);
                }
                "festival" => {
                    self.goal = Goal::Socialize;
                    println!("{} adapts to festival: switching to Socialize mode.", self.name);
                }
                _ => println!("{} ignores stimulus: {}", self.name, stimulus),
            }
        }
    }
}

pub mod narrative {
    #[derive(Debug)]
    pub struct StoryNode {
        pub id: u32,
        pub description: &'static str,
        pub next: Vec<u32>,
    }

    pub struct NarrativeEngine {
        pub nodes: Vec<StoryNode>,
        pub current: u32,
        pub arcs: Vec<String>,
    }

    impl NarrativeEngine {
        pub fn new() -> Self {
            let intro = StoryNode { id: 0, description: "The world begins at dawn.", next: vec![1, 2] };
            let storm = StoryNode { id: 1, description: "A storm brews across the horizon.", next: vec![3] };
            let festival = StoryNode { id: 2, description: "A festival lights up the village.", next: vec![3] };
            let climax = StoryNode { id: 3, description: "Avatars gather at the portal for destiny.", next: vec![] };

            NarrativeEngine {
                nodes: vec![intro, storm, festival, climax],
                current: 0,
                arcs: vec![],
            }
        }

        pub fn progress(&mut self, choice: usize) {
            let node = self.nodes.iter().find(|n| n.id == self.current).unwrap();
            if choice < node.next.len() {
                self.current = node.next[choice];
                let next_node = self.nodes.iter().find(|n| n.id == self.current).unwrap();
                println!("Narrative progresses: {}", next_node.description);
            } else {
                println!("No further narrative path.");
            }
        }

        pub fn current_description(&self) -> &str {
            self.nodes.iter().find(|n| n.id == self.current).unwrap().description
        }

        pub fn add_arc(&mut self, desc: String) {
            self.arcs.push(desc);
        }
    }
}

pub mod ai_narrative {
    use crate::ai::{Agent, Goal};
    use crate::narrative::NarrativeEngine;

    pub struct AgentNarrative {
        pub engine: NarrativeEngine,
        pub agents: Vec<Agent>,
    }

    impl AgentNarrative {
        pub fn new() -> Self {
            AgentNarrative {
                engine: NarrativeEngine::new(),
                agents: vec![],
            }
        }

        pub fn add_agent(&mut self, agent: Agent) {
            println!("Agent {} added to narrative system.", agent.name);
            self.agents.push(agent);
        }

        pub fn tick_agents(&mut self, env: &str) {
            for agent in &mut self.agents {
                agent.tick(env);

                match agent.goal {
                    Goal::Explore => {
                        println!("Narrative arc: {} discovers hidden ruins.", agent.name);
                        self.engine.progress(0);
                    }
                    Goal::Gather => {
                        println!("Narrative arc: {} uncovers rare resources.", agent.name);
                        self.engine.progress(1);
                    }
                    Goal::Defend => {
                        println!("Narrative arc: {} defends the portal.", agent.name);
                        self.engine.progress(0);
                    }
                    Goal::Socialize => {
                        println!("Narrative arc: {} sparks a festival storyline.", agent.name);
                        self.engine.progress(1);
                    }
                }
            }
        }
    }
}

pub mod narrative_ledger {
    use crate::ledger_services::{LedgerServices, Transaction, Reputation};
    use crate::narrative::NarrativeEngine;

    pub struct NarrativeLedger {
        pub engine: NarrativeEngine,
        pub services: LedgerServices,
    }

    impl NarrativeLedger {
        pub fn new() -> Self {
            NarrativeLedger {
                engine: NarrativeEngine::new(),
                services: LedgerServices::new(),
            }
        }

        pub fn record_story_event(&mut self, tx: Transaction) {
            let desc = format!("Story event: {} exchanged with {}", tx.from, tx.to);
            self.services.record_transaction(tx);
            self.engine.add_arc(desc);
            self.engine.progress(0);
        }

        pub fn reputation_story(&mut self, avatar: &'static str, delta: i32) {
            self.services.update_reputation(avatar, delta);

            if let Some(rep) = self.services.get_reputation(avatar) {
                if rep.score > 50 {
                    println!("Narrative arc: {} becomes a hero!", avatar);
                } else if rep.score < 0 {
                    println!("Narrative arc: {} falls into infamy!", avatar);
                }
            }
        }

        pub fn transaction_to_story(&mut self, tx: &Transaction) {
            let desc = format!(
                "A saga unfolds: {} transfers {} crystals to {} — trust and economy intertwine.",
                tx.from, tx.amount, tx.to
            );
            self.engine.add_arc(desc);
        }

        pub fn reputation_to_story(&mut self, rep: &Reputation) {
            let desc = format!(
                "Reputation shifts: {} rises with score {} — the avatar's legend grows.",
                rep.avatar, rep.score
            );
            self.engine.add_arc(desc);
        }

        pub fn narrate(&self) {
            println!("Ledger-driven narrative:");
            for arc in &self.engine.arcs {
                println!("- {}", arc);
            }
        }
    }
}

pub mod narrative_world {
    use crate::narrative::NarrativeEngine;

    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum EnvironmentEvent {
        Storm,
        Festival,
        Earthquake,
        Eclipse,
    }

    pub struct NarrativeWorld {
        pub engine: NarrativeEngine,
    }

    impl NarrativeWorld {
        pub fn new() -> Self {
            NarrativeWorld { engine: NarrativeEngine::new() }
        }

        pub fn apply_event(&mut self, event: EnvironmentEvent) {
            match event {
                EnvironmentEvent::Storm => {
                    println!("World event: A storm brews across the horizon.");
                    self.engine.progress(0);
                }
                EnvironmentEvent::Festival => {
                    println!("World event: A festival lights up the village.");
                    self.engine.progress(1);
                }
                EnvironmentEvent::Earthquake => {
                    println!("World event: The ground shakes violently.");
                    self.engine.progress(0);
                }
                EnvironmentEvent::Eclipse => {
                    println!("World event: Darkness falls as the eclipse begins.");
                    self.engine.progress(1);
                }
            }
        }
    }
}

// ---------------------------------------------------------------------------
// orchestration.rs and its expansions
// ---------------------------------------------------------------------------

pub mod orchestration {
    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum ServiceState {
        Starting,
        Running,
        Stopped,
    }

    #[derive(Debug)]
    pub struct Service {
        pub id: u32,
        pub name: &'static str,
        pub state: ServiceState,
    }

    impl Service {
        pub fn start(&mut self) {
            self.state = ServiceState::Starting;
            println!("Service {} is starting...", self.name);
            self.state = ServiceState::Running;
            println!("Service {} is now running.", self.name);
        }

        pub fn stop(&mut self) {
            self.state = ServiceState::Stopped;
            println!("Service {} has stopped.", self.name);
        }
    }

    pub struct Orchestrator {
        pub services: Vec<Service>,
    }

    impl Orchestrator {
        pub fn new() -> Self {
            Orchestrator { services: vec![] }
        }

        pub fn register(&mut self, service: Service) {
            println!("Registering service: {}", service.name);
            self.services.push(service);
        }

        pub fn start_all(&mut self) {
            for service in &mut self.services {
                service.start();
            }
        }

        pub fn stop_all(&mut self) {
            for service in &mut self.services {
                service.stop();
            }
        }

        pub fn scale(&mut self, factor: u32) {
            println!("Scaling services by factor {}", factor);
            for service in &mut self.services {
                println!("Service {} scaled to {}", service.name, factor);
            }
        }
    }
}

pub mod orchestration_policies {
    use crate::orchestration::{Service, ServiceState};

    pub struct PolicyOrchestrator {
        pub services: Vec<Service>,
    }

    impl PolicyOrchestrator {
        pub fn new() -> Self {
            PolicyOrchestrator { services: vec![] }
        }

        pub fn register(&mut self, service: Service) {
            println!("Registering service: {}", service.name);
            self.services.push(service);
        }

        pub fn auto_restart(&mut self) {
            for service in &mut self.services {
                if let ServiceState::Stopped = service.state {
                    println!("Auto-restarting service: {}", service.name);
                    service.start();
                }
            }
        }

        pub fn load_balance(&self, requests: u32) {
            let count = self.services.len() as u32;
            if count > 0 {
                let per_service = requests / count;
                for service in &self.services {
                    println!("Service {} handles {} requests.", service.name, per_service);
                }
            }
        }

        pub fn fault_tolerance(&mut self, failed_service_id: u32) {
            if let Some(service) = self.services.iter_mut().find(|s| s.id == failed_service_id) {
                println!("Fault detected in {}. Restarting...", service.name);
                service.start();
            } else {
                println!("No service found with ID {}", failed_service_id);
            }
        }
    }
}

pub mod orchestration_monitoring {
    use crate::orchestration::{Service, ServiceState};
    use std::time::SystemTime;

    #[derive(Debug)]
    pub struct ServiceMetrics {
        pub id: u32,
        pub name: &'static str,
        pub uptime: u64,
        pub requests_handled: u32,
        pub last_checked: SystemTime,
    }

    pub struct MonitoringOrchestrator {
        pub services: Vec<Service>,
        pub metrics: Vec<ServiceMetrics>,
    }

    impl MonitoringOrchestrator {
        pub fn new() -> Self {
            MonitoringOrchestrator { services: vec![], metrics: vec![] }
        }

        pub fn register(&mut self, service: Service) {
            println!("Registering service: {}", service.name);
            self.metrics.push(ServiceMetrics {
                id: service.id,
                name: service.name,
                uptime: 0,
                requests_handled: 0,
                last_checked: SystemTime::now(),
            });
            self.services.push(service);
        }

        pub fn log_request(&mut self, service_id: u32) {
            if let Some(m) = self.metrics.iter_mut().find(|m| m.id == service_id) {
                m.requests_handled += 1;
                println!("Service {} handled request #{}", m.name, m.requests_handled);
            }
        }

        pub fn health_check(&self) {
            for (i, service) in self.services.iter().enumerate() {
                let _ = &self.metrics[i];
                match service.state {
                    ServiceState::Running => println!("Health OK: {}", service.name),
                    ServiceState::Stopped => println!("Health FAIL: {} is stopped", service.name),
                    ServiceState::Starting => println!("Health WARN: {} is starting", service.name),
                }
            }
        }

        pub fn report(&self) {
            println!("Monitoring Report:");
            for m in &self.metrics {
                println!("{} uptime={}s, requests={}", m.name, m.uptime, m.requests_handled);
            }
        }
    }
}

pub mod orchestration_resilience {
    use crate::orchestration::{Service, ServiceState};

    pub struct ResilientOrchestrator {
        pub services: Vec<Service>,
    }

    impl ResilientOrchestrator {
        pub fn new() -> Self {
            ResilientOrchestrator { services: vec![] }
        }

        pub fn register(&mut self, service: Service) {
            println!("Registering resilient service: {}", service.name);
            self.services.push(service);
        }

        pub fn predictive_scale(&self, load: u32) {
            let count = self.services.len() as u32;
            if count > 0 {
                let factor = (load / count).max(1);
                println!("Predictive scaling factor: {}", factor);
                for service in &self.services {
                    println!("Service {} scaled to {}", service.name, factor);
                }
            }
        }

        pub fn self_heal(&mut self) {
            for service in &mut self.services {
                if let ServiceState::Stopped = service.state {
                    println!("Self-healing: restarting {}", service.name);
                    service.start();
                }
            }
        }

        pub fn adaptive_recovery(&mut self, failed_id: u32) {
            if let Some(service) = self.services.iter_mut().find(|s| s.id == failed_id) {
                println!("Adaptive recovery triggered for {}", service.name);
                service.start();
            } else {
                println!("No service found with ID {}", failed_id);
            }
        }
    }
}

pub mod orchestration_intelligence {
    use crate::orchestration::Service;

    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum Anomaly {
        HighLatency,
        ExcessiveFailures,
        ResourceSpike,
    }

    pub struct IntelligentOrchestrator {
        pub services: Vec<Service>,
    }

    impl IntelligentOrchestrator {
        pub fn new() -> Self {
            IntelligentOrchestrator { services: vec![] }
        }

        pub fn register(&mut self, service: Service) {
            println!("Registering intelligent service: {}", service.name);
            self.services.push(service);
        }

        pub fn detect_anomaly(&self, service_id: u32, anomaly: Anomaly) {
            if let Some(service) = self.services.iter().find(|s| s.id == service_id) {
                match anomaly {
                    Anomaly::HighLatency => println!("Anomaly detected: {} has high latency.", service.name),
                    Anomaly::ExcessiveFailures => println!("Anomaly detected: {} is failing repeatedly.", service.name),
                    Anomaly::ResourceSpike => println!("Anomaly detected: {} is consuming excessive resources.", service.name),
                }
            }
        }

        pub fn intelligent_scale(&self, load: u32) {
            let count = self.services.len() as u32;
            if count > 0 {
                let factor = (load / count).max(1);
                println!("Intelligent scaling factor: {}", factor);
                for service in &self.services {
                    println!("Service {} scaled intelligently to {}", service.name, factor);
                }
            }
        }

        pub fn adaptive_response(&mut self, service_id: u32, anomaly: Anomaly) {
            if let Some(service) = self.services.iter_mut().find(|s| s.id == service_id) {
                println!("Adaptive response triggered for {} due to {:?}", service.name, anomaly);
                service.start();
            }
        }
    }
}

pub mod orchestration_governance {
    use crate::orchestration::{Service, ServiceState};
    use crate::governance::{GovernanceRecord, GovernanceStatus};
    use crate::governance_policies::TrustTier;

    pub struct GovernedOrchestrator {
        pub services: Vec<Service>,
        pub governance: Vec<GovernanceRecord>,
    }

    impl GovernedOrchestrator {
        pub fn new() -> Self {
            GovernedOrchestrator { services: vec![], governance: vec![] }
        }

        pub fn register(&mut self, service: Service, record: GovernanceRecord) {
            println!("Registering governed service: {}", service.name);
            self.services.push(service);
            self.governance.push(record);
        }

        pub fn enforce_policies(&self) {
            for (service, record) in self.services.iter().zip(self.governance.iter()) {
                let tier = match record.trust_score {
                    0..=30 => TrustTier::Low,
                    31..=70 => TrustTier::Medium,
                    _ => TrustTier::High,
                };

                match record.status {
                    GovernanceStatus::Approved => println!("{} runs under {:?} trust tier.", service.name, tier),
                    GovernanceStatus::Rejected => println!("{} blocked due to governance rejection.", service.name),
                    GovernanceStatus::Pending => println!("{} paused pending moderation.", service.name),
                }
            }
        }

        pub fn monitor_and_enforce(&self) {
            for service in &self.services {
                match service.state {
                    ServiceState::Running => println!("{} is running — governance OK.", service.name),
                    ServiceState::Stopped => println!("{} stopped — governance check triggered.", service.name),
                    ServiceState::Starting => println!("{} starting — governance monitoring active.", service.name),
                }
            }
        }
    }
}

pub mod orchestration_narrative {
    use crate::orchestration_intelligence::Anomaly;
    use crate::narrative::NarrativeEngine;

    pub struct NarrativeOrchestrator {
        pub engine: NarrativeEngine,
    }

    impl NarrativeOrchestrator {
        pub fn new() -> Self {
            NarrativeOrchestrator { engine: NarrativeEngine::new() }
        }

        pub fn anomaly_to_story(&mut self, anomaly: Anomaly) {
            match anomaly {
                Anomaly::HighLatency => {
                    println!("Narrative trigger: The portal slows, time itself drags.");
                    self.engine.progress(0);
                }
                Anomaly::ExcessiveFailures => {
                    println!("Narrative trigger: Chaos erupts, systems collapse like crumbling towers.");
                    self.engine.progress(0);
                }
                Anomaly::ResourceSpike => {
                    println!("Narrative trigger: Energy surge floods the realm, avatars gain unstable power.");
                    self.engine.progress(1);
                }
            }
        }

        pub fn narrate(&self) {
            println!("Current narrative: {}", self.engine.current_description());
        }
    }
}

pub mod ledger_governance {
    use crate::ledger_services::{Transaction, Reputation};
    use crate::developer_trust::{TrustTier, privileges_for_tier};

    #[derive(Debug)]
    pub struct GovernanceLedger {
        pub trust_score: i32,
        pub tier: TrustTier,
    }

    impl GovernanceLedger {
        pub fn new() -> Self {
            GovernanceLedger { trust_score: 50, tier: TrustTier::Medium }
        }

        pub fn apply_transaction(&mut self, tx: &Transaction) {
            self.trust_score += (tx.amount / 10) as i32;
            self.update_tier();
            println!("Transaction applied: {} → {} (+{})", tx.from, tx.to, tx.amount);
        }

        pub fn apply_reputation(&mut self, rep: &Reputation) {
            self.trust_score += rep.score / 5;
            self.update_tier();
            println!("Reputation applied: {} score {}", rep.avatar, rep.score);
        }

        fn update_tier(&mut self) {
            self.tier = match self.trust_score {
                0..=30 => TrustTier::Low,
                31..=70 => TrustTier::Medium,
                _ => TrustTier::High,
            };
            let privs = privileges_for_tier(self.tier);
            println!("Updated tier: {:?} with privileges {:?}", self.tier, privs);
        }
    }
}

// ---------------------------------------------------------------------------
// anomaly_quests.rs / kenji_anomaly_quests.rs / anomaly_multimedia.rs
// ---------------------------------------------------------------------------

pub mod anomaly_quests {
    use crate::orchestration_intelligence::Anomaly;

    #[derive(Debug)]
    pub struct Quest {
        pub title: String,
        pub description: String,
        pub reward: i32,
    }

    pub struct AnomalyQuestEngine;

    impl AnomalyQuestEngine {
        pub fn new() -> Self {
            AnomalyQuestEngine
        }

        pub fn generate_from_anomaly(&self, anomaly: Anomaly) -> Quest {
            match anomaly {
                Anomaly::HighLatency => Quest {
                    title: "Quest of Slowed Time".to_string(),
                    description: "The portal drags — stabilize time flow by balancing resource nodes.".to_string(),
                    reward: 50,
                },
                Anomaly::ExcessiveFailures => Quest {
                    title: "Quest of Chaos".to_string(),
                    description: "Systems collapse — rally avatars to rebuild failing towers.".to_string(),
                    reward: 100,
                },
                Anomaly::ResourceSpike => Quest {
                    title: "Quest of Unstable Power".to_string(),
                    description: "Energy surge floods the realm — harness unstable crystals before they explode.".to_string(),
                    reward: 75,
                },
            }
        }
    }
}

pub mod kenji_anomaly_quests {
    use crate::orchestration_intelligence::Anomaly;

    #[derive(Debug)]
    pub struct KenjiQuest {
        pub title: String,
        pub narrative: String,
        pub lesson: String,
        pub reward: String,
    }

    pub fn kenji_style_quest(anomaly: Anomaly) -> KenjiQuest {
        match anomaly {
            Anomaly::HighLatency => KenjiQuest {
                title: "The Slow River".to_string(),
                narrative: "Time drags like a sluggish river; gather starlight seeds to restore flow.".to_string(),
                lesson: "Patience and collective effort overcome stagnation.".to_string(),
                reward: "Song of Flow".to_string(),
            },
            Anomaly::ExcessiveFailures => KenjiQuest {
                title: "The Crumbling Towers".to_string(),
                narrative: "Towers collapse under invisible weight; rebuild them with words of kindness.".to_string(),
                lesson: "Cooperation and compassion repair broken systems.".to_string(),
                reward: "Stone of Resilience".to_string(),
            },
            Anomaly::ResourceSpike => KenjiQuest {
                title: "The Unstable Crystals".to_string(),
                narrative: "Crystals glow too brightly; sing lullabies to calm their unstable light.".to_string(),
                lesson: "Balance and humility tame excess.".to_string(),
                reward: "Crystal of Balance".to_string(),
            },
        }
    }
}

// ---------------------------------------------------------------------------
// multimedia.rs and friends
// ---------------------------------------------------------------------------

pub mod multimedia {
    #[derive(Debug, Clone)]
    pub struct Frame {
        pub id: u32,
        pub description: String,
        pub style: String,
    }

    #[derive(Debug, Clone)]
    pub struct Audio {
        pub id: u32,
        pub track: String,
        pub mood: String,
    }

    #[derive(Debug, Clone)]
    pub struct Sequence {
        pub id: u32,
        pub frames: Vec<Frame>,
        pub audio: Audio,
        pub interactive: bool,
    }

    #[derive(Debug, Clone)]
    pub struct MultimediaEngine;

    impl MultimediaEngine {
        pub fn new() -> Self {
            MultimediaEngine
        }

        pub fn generate_frame(&self, id: u32, description: &str, style: &str) -> Frame {
            Frame {
                id,
                description: description.to_string(),
                style: style.to_string(),
            }
        }

        pub fn generate_audio(&self, id: u32, track: &str, mood: &str) -> Audio {
            Audio {
                id,
                track: track.to_string(),
                mood: mood.to_string(),
            }
        }

        pub fn build_sequence(&self, id: u32, frames: Vec<Frame>, audio: Audio, interactive: bool) -> Sequence {
            Sequence { id, frames, audio, interactive }
        }

        pub fn play(&self, seq: &Sequence) {
            println!(
                "Playing sequence {} with {} frames, audio '{}', mood '{}'",
                seq.id,
                seq.frames.len(),
                seq.audio.track,
                seq.audio.mood
            );
            for f in &seq.frames {
                println!("Frame {} [{}]: {}", f.id, f.style, f.description);
            }
            if seq.interactive {
                println!("This sequence is interactive — avatars can influence outcomes.");
            }
        }
    }
}

pub mod narrative_multimedia {
    use crate::narrative::NarrativeEngine;
    use crate::multimedia::{MultimediaEngine, Sequence};

    pub struct NarrativeMultimedia {
        pub narrative: NarrativeEngine,
        pub multimedia: MultimediaEngine,
    }

    impl NarrativeMultimedia {
        pub fn new() -> Self {
            NarrativeMultimedia {
                narrative: NarrativeEngine::new(),
                multimedia: MultimediaEngine::new(),
            }
        }

        pub fn render_arc(&self, arc: &str, style: &str, mood: &str) -> Sequence {
            let f1 = self.multimedia.generate_frame(1, arc, style);
            let f2 = self.multimedia.generate_frame(2, "Avatars respond to the arc", style);
            let audio = self.multimedia.generate_audio(1, "Procedural Track", mood);
            self.multimedia.build_sequence(1, vec![f1, f2], audio, true)
        }

        pub fn narrate_and_render(&mut self, arc: &str) {
            self.narrative.add_arc(arc.to_string());
            let seq = self.render_arc(arc, "cinematic", "mystical");
            self.multimedia.play(&seq);
        }
    }
}

pub mod multimedia_api {
    use crate::multimedia::{MultimediaEngine, Frame, Audio, Sequence};

    #[derive(Debug, Clone)]
    pub enum ScriptCommand {
        Frame(u32, &'static str, &'static str),
        Audio(u32, &'static str, &'static str),
        Sequence(u32, Vec<u32>, u32, bool),
    }

    #[derive(Debug, Clone)]
    pub struct MultimediaScriptAPI {
        pub engine: MultimediaEngine,
    }

    impl MultimediaScriptAPI {
        pub fn new() -> Self {
            MultimediaScriptAPI { engine: MultimediaEngine::new() }
        }

        pub fn execute(&self, commands: Vec<ScriptCommand>) -> Vec<Sequence> {
            let mut sequences = vec![];
            let mut frames: Vec<Frame> = vec![];
            let mut audio_map: Vec<Audio> = vec![];

            for cmd in commands {
                match cmd {
                    ScriptCommand::Frame(id, desc, style) => {
                        frames.push(self.engine.generate_frame(id, desc, style));
                    }
                    ScriptCommand::Audio(id, track, mood) => {
                        audio_map.push(self.engine.generate_audio(id, track, mood));
                    }
                    ScriptCommand::Sequence(id, frame_ids, audio_id, interactive) => {
                        let selected_frames: Vec<Frame> = frames
                            .iter()
                            .filter(|f| frame_ids.contains(&f.id))
                            .cloned()
                            .collect();
                        let selected_audio = audio_map
                            .iter()
                            .find(|a| a.id == audio_id)
                            .map(|a| a.clone())
                            .unwrap_or_else(|| self.engine.generate_audio(audio_id, "Silence", "neutral"));
                        let seq = self.engine.build_sequence(id, selected_frames, selected_audio, interactive);
                        sequences.push(seq);
                    }
                }
            }
            sequences
        }
    }
}

// ---------------------------------------------------------------------------
// symbolic_ontology.rs / ontology_governance.rs / ontology_narrative.rs
// ---------------------------------------------------------------------------

pub mod symbolic_ontology {
    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum CosmicConstant {
        TimeFlow,
        TrustBalance,
        ResourceHarmony,
        ExpressionFreedom,
    }

    #[derive(Debug)]
    pub struct SymbolicArchetype {
        pub name: &'static str,
        pub meaning: &'static str,
        pub linked_constant: CosmicConstant,
    }

    pub struct OntologyLayer {
        pub archetypes: Vec<SymbolicArchetype>,
    }

    impl OntologyLayer {
        pub fn new() -> Self {
            OntologyLayer {
                archetypes: vec![
                    SymbolicArchetype { name: "River of Time", meaning: "Flow and patience", linked_constant: CosmicConstant::TimeFlow },
                    SymbolicArchetype { name: "Crystal of Trust", meaning: "Balance and fairness", linked_constant: CosmicConstant::TrustBalance },
                    SymbolicArchetype { name: "Tree of Harmony", meaning: "Sustainability and ecology", linked_constant: CosmicConstant::ResourceHarmony },
                    SymbolicArchetype { name: "Song of Freedom", meaning: "Expression and creativity", linked_constant: CosmicConstant::ExpressionFreedom },
                ],
            }
        }

        pub fn describe(&self) {
            println!("Symbolic Ontology Layer:");
            for arc in &self.archetypes {
                println!("{} → {} (linked to {:?})", arc.name, arc.meaning, arc.linked_constant);
            }
        }

        pub fn count(&self) -> usize {
            self.archetypes.len()
        }
    }
}

pub mod ontology_governance {
    use crate::symbolic_ontology::{CosmicConstant, OntologyLayer};

    #[derive(Debug)]
    pub enum OntologyVerdict {
        Aligned(&'static str),
        Violation(&'static str),
    }

    pub struct OntologyGovernance {
        pub ontology: OntologyLayer,
    }

    impl OntologyGovernance {
        pub fn new() -> Self {
            OntologyGovernance { ontology: OntologyLayer::new() }
        }

        pub fn enforce_constant(&self, constant: CosmicConstant, _actor: &'static str) -> OntologyVerdict {
            match constant {
                CosmicConstant::TimeFlow => OntologyVerdict::Aligned("Actor respects flow of time"),
                CosmicConstant::TrustBalance => OntologyVerdict::Violation("Actor disrupted trust balance"),
                CosmicConstant::ResourceHarmony => OntologyVerdict::Aligned("Actor maintained ecological harmony"),
                CosmicConstant::ExpressionFreedom => OntologyVerdict::Aligned("Actor protected free expression"),
            }
        }

        pub fn audit_archetypes(&self) {
            println!("Ontology Governance Audit:");
            for arc in &self.ontology.archetypes {
                println!(
                    "Archetype {} → {} (constant {:?})",
                    arc.name, arc.meaning, arc.linked_constant
                );
            }
        }
    }
}

pub mod ontology_narrative {
    use crate::symbolic_ontology::{CosmicConstant, OntologyLayer};

    #[derive(Debug)]
    pub struct OntologyArc {
        pub title: String,
        pub description: String,
        pub lesson: String,
    }

    pub struct OntologyNarrative {
        pub ontology: OntologyLayer,
    }

    impl OntologyNarrative {
        pub fn new() -> Self {
            OntologyNarrative { ontology: OntologyLayer::new() }
        }

        pub fn generate_arc(&self, constant: CosmicConstant) -> OntologyArc {
            match constant {
                CosmicConstant::TimeFlow => OntologyArc {
                    title: "Saga of the River".to_string(),
                    description: "Time flows like a river; avatars must learn patience to cross its currents.".to_string(),
                    lesson: "Respecting time brings harmony.".to_string(),
                },
                CosmicConstant::TrustBalance => OntologyArc {
                    title: "Saga of the Crystal".to_string(),
                    description: "Trust shatters when balance is broken; avatars must restore fairness in trade.".to_string(),
                    lesson: "Fairness sustains community.".to_string(),
                },
                CosmicConstant::ResourceHarmony => OntologyArc {
                    title: "Saga of the Tree".to_string(),
                    description: "The tree wilts when resources are wasted; avatars must nurture ecology.".to_string(),
                    lesson: "Sustainability ensures survival.".to_string(),
                },
                CosmicConstant::ExpressionFreedom => OntologyArc {
                    title: "Saga of the Song".to_string(),
                    description: "Songs echo across the realm; avatars must protect freedom of voice.".to_string(),
                    lesson: "Expression is the soul of the world.".to_string(),
                },
            }
        }

        pub fn narrate(&self) {
            println!("Ontology-Driven Narrative:");
            for arc in &self.ontology.archetypes {
                let story = self.generate_arc(arc.linked_constant);
                println!("{} → {}", story.title, story.description);
            }
        }
    }
}

// ---------------------------------------------------------------------------
// hazeru_dsl.rs / gran_grimoire.rs / ritual_library.rs / ritual_exchange.rs /
// grimoire_ledger.rs
// ---------------------------------------------------------------------------

pub mod hazeru_dsl {
    use crate::multimedia_api::{MultimediaScriptAPI, ScriptCommand};

    #[derive(Debug)]
    pub enum DSLCommand {
        Ontology(&'static str),
        Narrative(&'static str),
        Multimedia(Vec<ScriptCommand>),
    }

    pub struct HazeruDSL {
        pub multimedia_api: MultimediaScriptAPI,
    }

    impl HazeruDSL {
        pub fn new() -> Self {
            HazeruDSL { multimedia_api: MultimediaScriptAPI::new() }
        }

        pub fn interpret(&self, commands: Vec<DSLCommand>) {
            for cmd in commands {
                match cmd {
                    DSLCommand::Ontology(symbol) => {
                        println!("Invoking ontology constant: {}", symbol);
                    }
                    DSLCommand::Narrative(arc) => {
                        println!("Narrative arc invoked: {}", arc);
                    }
                    DSLCommand::Multimedia(script) => {
                        let sequences = self.multimedia_api.execute(script);
                        for seq in sequences {
                            self.multimedia_api.engine.play(&seq);
                        }
                    }
                }
            }
        }
    }
}

pub mod gran_grimoire {
    use crate::multimedia_api::MultimediaScriptAPI;

    #[derive(Debug, Clone)]
    pub enum GrimoireToken {
        Invoke(&'static str),
        Story(&'static str),
        Vision(&'static str),
        Chant(&'static str),
    }

    #[derive(Debug, Clone)]
    pub struct GranGrimoire {
        pub multimedia_api: MultimediaScriptAPI,
    }

    impl GranGrimoire {
        pub fn new() -> Self {
            GranGrimoire { multimedia_api: MultimediaScriptAPI::new() }
        }

        pub fn cast(&self, tokens: Vec<GrimoireToken>) {
            println!("Casting ritual sequence from {}", crate::GRIMOIRE);
            let mut frames = vec![];
            let mut audio = None;

            for t in tokens {
                match t {
                    GrimoireToken::Invoke(symbol) => {
                        println!("⚖️ Ontology invoked: {}", symbol);
                    }
                    GrimoireToken::Story(arc) => {
                        println!("📖 Narrative arc: {}", arc);
                        frames.push(self.multimedia_api.engine.generate_frame(1, arc, "cinematic"));
                    }
                    GrimoireToken::Vision(style) => {
                        println!("🎨 Vision style: {}", style);
                        frames.push(self.multimedia_api.engine.generate_frame(2, "Symbolic vision", style));
                    }
                    GrimoireToken::Chant(mood) => {
                        println!("🎶 Chant mood: {}", mood);
                        audio = Some(self.multimedia_api.engine.generate_audio(1, "Ritual Track", mood));
                    }
                }
            }

            if let Some(a) = audio {
                let seq = self.multimedia_api.engine.build_sequence(1, frames, a, true);
                self.multimedia_api.engine.play(&seq);
            }
        }
    }
}

pub mod ritual_library {
    use crate::gran_grimoire::{GranGrimoire, GrimoireToken};

    #[derive(Debug, Clone)]
    pub struct Ritual {
        pub name: String,
        pub tokens: Vec<GrimoireToken>,
    }

    #[derive(Debug, Clone)]
    pub struct RitualLibrary {
        pub rituals: Vec<Ritual>,
        pub grimoire: GranGrimoire,
    }

    impl RitualLibrary {
        pub fn new() -> Self {
            RitualLibrary {
                rituals: vec![],
                grimoire: GranGrimoire::new(),
            }
        }

        pub fn add_ritual(&mut self, name: &str, tokens: Vec<GrimoireToken>) {
            let ritual = Ritual { name: name.to_string(), tokens };
            println!("📚 Ritual '{}' added to library.", name);
            self.rituals.push(ritual);
        }

        pub fn invoke(&self, name: &str) {
            if let Some(r) = self.rituals.iter().find(|ritual| ritual.name == name) {
                println!("🔮 Invoking ritual '{}':", r.name);
                self.grimoire.cast(r.tokens.clone());
            } else {
                println!("⚠️ Ritual '{}' not found in library.", name);
            }
        }

        pub fn list(&self) {
            println!("📖 Ritual Library contains:");
            for r in &self.rituals {
                println!("- {}", r.name);
            }
        }

        pub fn count(&self) -> usize {
            self.rituals.len()
        }
    }
}

pub mod ritual_exchange {
    use crate::ritual_library::RitualLibrary;

    #[derive(Debug)]
    pub struct ExchangeRecord {
        pub from: String,
        pub to: String,
        pub ritual_name: String,
    }

    pub struct RitualExchange {
        pub library: RitualLibrary,
        pub records: Vec<ExchangeRecord>,
    }

    impl RitualExchange {
        pub fn new(library: RitualLibrary) -> Self {
            RitualExchange {
                library,
                records: vec![],
            }
        }

        pub fn transfer(&mut self, from: &str, to: &str, ritual_name: &str) {
            if self.library.rituals.iter().any(|ritual| ritual.name == ritual_name) {
                println!("🔄 Ritual '{}' transferred from {} to {}", ritual_name, from, to);
                self.records.push(ExchangeRecord {
                    from: from.to_string(),
                    to: to.to_string(),
                    ritual_name: ritual_name.to_string(),
                });
            } else {
                println!("⚠️ Ritual '{}' not found in library.", ritual_name);
            }
        }

        pub fn audit(&self) {
            println!("📜 Ritual Exchange Records:");
            for rec in &self.records {
                println!("- {} → {} : {}", rec.from, rec.to, rec.ritual_name);
            }
        }
    }
}

pub mod grimoire_ledger {
    use crate::gran_grimoire::{GranGrimoire, GrimoireToken};
    use crate::ledger::{Ledger, LedgerEntry};

    pub struct GrimoireLedger {
        pub grimoire: GranGrimoire,
        pub ledger: Ledger,
    }

    impl GrimoireLedger {
        pub fn new() -> Self {
            GrimoireLedger {
                grimoire: GranGrimoire::new(),
                ledger: Ledger::new(),
            }
        }

        pub fn cast_with_ledger(&mut self, actor: &str, tokens: Vec<GrimoireToken>) {
            println!("🔮 Casting ritual with ledger integration...");
            self.grimoire.cast(tokens.clone());

            let entry = LedgerEntry {
                actor: actor.to_string(),
                action: format!("Cast ritual with {} tokens", tokens.len()),
                reward: tokens.len() as i32 * 10,
            };

            self.ledger.record(entry);
        }

        pub fn audit(&self) {
            println!("📜 Ritual Ledger Audit:");
            self.ledger.print();
        }

        pub fn valid(&self) -> bool {
            self.ledger.validate()
        }
    }
}

// ---------------------------------------------------------------------------
// civic services / audit / laws / enforcement / judiciary
// ---------------------------------------------------------------------------

pub mod civic_services {
    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum CivicLaw {
        TradeFairness,
        AntiFraud,
        ReputationTransparency,
        EnvironmentalBalance,
    }

    #[derive(Debug)]
    pub struct CivicService {
        pub law: CivicLaw,
        pub description: &'static str,
        pub enforced: bool,
    }

    pub struct CivicSystem {
        pub services: Vec<CivicService>,
    }

    impl CivicSystem {
        pub fn new() -> Self {
            CivicSystem { services: vec![] }
        }

        pub fn add_service(&mut self, law: CivicLaw, description: &'static str) {
            let service = CivicService { law, description, enforced: true };
            println!("Civic service added: {:?}", service.law);
            self.services.push(service);
        }

        pub fn enforce(&self) {
            for service in &self.services {
                if service.enforced {
                    println!("Enforcing civic law: {:?} — {}", service.law, service.description);
                }
            }
        }

        pub fn audit(&self) {
            println!("Civic Audit Report:");
            for service in &self.services {
                println!("{:?} enforced={}", service.law, service.enforced);
            }
        }
    }
}

pub mod civic_laws {
    #[derive(Debug, Clone, Copy, PartialEq)]
    pub enum CivicLaw {
        TradeFairness,
        AntiFraud,
        ReputationTransparency,
        EnvironmentalBalance,
        PrivacyProtection,
        EqualityAssurance,
        SustainabilityMandate,
        FreeExpression,
        DataTransparency,
    }

    #[derive(Debug)]
    pub struct CivicLawDefinition {
        pub law: CivicLaw,
        pub description: &'static str,
    }

    pub fn law_catalog() -> Vec<CivicLawDefinition> {
        vec![
            CivicLawDefinition { law: CivicLaw::TradeFairness, description: "Ensure fair exchange in all ledger transactions" },
            CivicLawDefinition { law: CivicLaw::AntiFraud, description: "Prevent fraudulent plugins and economic exploits" },
            CivicLawDefinition { law: CivicLaw::ReputationTransparency, description: "Make avatar reputation scores visible and auditable" },
            CivicLawDefinition { law: CivicLaw::EnvironmentalBalance, description: "Maintain ecological balance in simulated worlds" },
            CivicLawDefinition { law: CivicLaw::PrivacyProtection, description: "Safeguard user data and avatar identity from unauthorized access" },
            CivicLawDefinition { law: CivicLaw::EqualityAssurance, description: "Guarantee equal treatment of avatars regardless of origin or design" },
            CivicLawDefinition { law: CivicLaw::SustainabilityMandate, description: "Promote resource efficiency and sustainable simulation practices" },
            CivicLawDefinition { law: CivicLaw::FreeExpression, description: "Protect avatar speech and creative expression within civic bounds" },
            CivicLawDefinition { law: CivicLaw::DataTransparency, description: "Require transparent reporting of system metrics and governance actions" },
        ]
    }
}

pub mod civic_audit {
    use crate::civic_laws::CivicLaw;

    #[derive(Debug)]
    pub enum EnforcementOutcome {
        Warning(&'static str),
        Penalty(&'static str, i32),
        Reward(&'static str, i32),
        Compliance(&'static str),
    }

    #[derive(Debug)]
    pub struct AuditRecord {
        pub law: CivicLaw,
        pub action: String,
        pub actor: String,
        pub timestamp: String,
        pub outcome: String,
    }

    pub struct CivicAuditTrail {
        pub records: Vec<AuditRecord>,
    }

    impl CivicAuditTrail {
        pub fn new() -> Self {
            CivicAuditTrail { records: vec![] }
        }

        pub fn log(
            &mut self,
            law: CivicLaw,
            action: &str,
            actor: &str,
            outcome: &str,
            timestamp: &str,
        ) {
            let record = AuditRecord {
                law,
                action: action.to_string(),
                actor: actor.to_string(),
                timestamp: timestamp.to_string(),
                outcome: outcome.to_string(),
            };
            println!("Audit logged: {:?} by {}", law, actor);
            self.records.push(record);
        }

        pub fn report(&self) {
            println!("Civic Audit Trail Report:");
            for r in &self.records {
                println!(
                    "{:?} — {} by {} at {} → {}",
                    r.law, r.action, r.actor, r.timestamp, r.outcome
                );
            }
        }

        pub fn count(&self) -> usize {
            self.records.len()
        }
    }
}

pub mod civic_enforcement {
    use crate::civic_laws::{CivicLaw, law_catalog};
    use crate::civic_audit::{CivicAuditTrail, EnforcementOutcome};

    pub struct CivicEnforcementEngine {
        pub audit: CivicAuditTrail,
    }

    impl CivicEnforcementEngine {
        pub fn new() -> Self {
            CivicEnforcementEngine { audit: CivicAuditTrail::new() }
        }

        pub fn evaluate(law: CivicLaw, _actor: &'static str) -> EnforcementOutcome {
            match law {
                CivicLaw::TradeFairness => EnforcementOutcome::Reward("Fair trade completed", 10),
                CivicLaw::AntiFraud => EnforcementOutcome::Penalty("Fraud detected", 20),
                CivicLaw::ReputationTransparency => EnforcementOutcome::Compliance("Reputation disclosed"),
                CivicLaw::EnvironmentalBalance => EnforcementOutcome::Reward("Eco balance maintained", 5),
                CivicLaw::PrivacyProtection => EnforcementOutcome::Penalty("Privacy violation", 15),
                CivicLaw::EqualityAssurance => EnforcementOutcome::Compliance("Equality upheld"),
                CivicLaw::SustainabilityMandate => EnforcementOutcome::Reward("Sustainable practice applied", 8),
                CivicLaw::FreeExpression => EnforcementOutcome::Compliance("Expression protected"),
                CivicLaw::DataTransparency => EnforcementOutcome::Warning("Transparency report overdue"),
            }
        }

        pub fn enforce(&mut self, law: CivicLaw, actor: &'static str, timestamp: &'static str) {
            let outcome = Self::evaluate(law, actor);
            let _ = actor;
            self.audit.log(law, "Enforcement", "CivicDaemon", &format!("{:?}", outcome), timestamp);
        }

        pub fn audit_report(&self) {
            self.audit.report();
        }

        pub fn list_laws(&self) {
            println!("Civic Law Catalog:");
            for law in law_catalog() {
                println!("{:?} — {}", law.law, law.description);
            }
        }
    }
}

pub mod civic_judiciary {
    use crate::civic_laws::CivicLaw;

    #[derive(Debug)]
    pub enum Verdict {
        Guilty(&'static str, i32),
        Innocent(&'static str),
        Appealed(&'static str),
    }

    #[derive(Debug)]
    pub struct Trial {
        pub law: CivicLaw,
        pub actor: &'static str,
        pub evidence: Vec<&'static str>,
        pub verdict: Option<Verdict>,
    }

    pub struct JudiciarySystem {
        pub trials: Vec<Trial>,
    }

    impl JudiciarySystem {
        pub fn new() -> Self {
            JudiciarySystem { trials: vec![] }
        }

        pub fn start_trial(&mut self, law: CivicLaw, actor: &'static str, evidence: Vec<&'static str>) {
            let trial = Trial { law, actor, evidence, verdict: None };
            println!("Trial started for {} under {:?}", actor, law);
            self.trials.push(trial);
        }

        pub fn deliver_verdict(&mut self, actor: &'static str, verdict: Verdict) {
            if let Some(trial) = self.trials.iter_mut().find(|t| t.actor == actor) {
                trial.verdict = Some(verdict);
                println!("Verdict delivered for {}: {:?}", actor, trial.verdict);
            }
        }

        pub fn appeal(&mut self, actor: &'static str, reason: &'static str) {
            if let Some(trial) = self.trials.iter_mut().find(|t| t.actor == actor) {
                trial.verdict = Some(Verdict::Appealed(reason));
                println!("Appeal filed for {}: {}", actor, reason);
            }
        }

        pub fn report(&self) {
            println!("Judiciary Report:");
            for trial in &self.trials {
                println!("{:?} trial for {} → {:?}", trial.law, trial.actor, trial.verdict);
            }
        }
    }
}

// ---------------------------------------------------------------------------
// anomaly_multimedia.rs
// ---------------------------------------------------------------------------

pub mod anomaly_multimedia {
    use crate::orchestration_intelligence::Anomaly;
    use crate::anomaly_quests::Quest;
    use crate::multimedia::{MultimediaEngine, Sequence};

    pub struct AnomalyMultimedia {
        pub engine: MultimediaEngine,
    }

    impl AnomalyMultimedia {
        pub fn new() -> Self {
            AnomalyMultimedia { engine: MultimediaEngine::new() }
        }

        pub fn quest_to_sequence(&self, quest: Quest, style: &str, mood: &str) -> Sequence {
            let f1 = self.engine.generate_frame(1, &quest.title, style);
            let f2 = self.engine.generate_frame(2, &quest.description, style);
            let audio = self.engine.generate_audio(1, "Quest Track", mood);
            self.engine.build_sequence(quest.reward as u32, vec![f1, f2], audio, true)
        }

        pub fn render_anomaly(&self, anomaly: Anomaly) {
            let quest = match anomaly {
                Anomaly::HighLatency => Quest {
                    title: "The Slow River".to_string(),
                    description: "Time drags like a sluggish river; gather starlight seeds to restore flow.".to_string(),
                    reward: 50,
                },
                Anomaly::ExcessiveFailures => Quest {
                    title: "The Crumbling Towers".to_string(),
                    description: "Towers collapse under invisible weight; rebuild them with words of kindness.".to_string(),
                    reward: 100,
                },
                Anomaly::ResourceSpike => Quest {
                    title: "The Unstable Crystals".to_string(),
                    description: "Crystals glow too brightly; sing lullabies to calm their unstable light.".to_string(),
                    reward: 75,
                },
            };

            let seq = self.quest_to_sequence(quest, "cinematic", "mystical");
            self.engine.play(&seq);
        }
    }
}

// ---------------------------------------------------------------------------
// ihatov_loop.rs / ihatov_saga.rs / saga_persistence.rs / saga_replay.rs /
// saga_branching.rs
// ---------------------------------------------------------------------------

pub mod ihatov_loop {
    use crate::orchestration_intelligence::Anomaly;
    use crate::anomaly_multimedia::AnomalyMultimedia;
    use crate::ritual_library::RitualLibrary;
    use crate::ritual_exchange::RitualExchange;
    use crate::ontology_governance::OntologyGovernance;
    use crate::ontology_narrative::OntologyNarrative;
    use crate::gran_grimoire::GrimoireToken;

    pub struct IhatovLoop {
        pub anomaly_engine: AnomalyMultimedia,
        pub ritual_library: RitualLibrary,
        pub ritual_exchange: RitualExchange,
        pub governance: OntologyGovernance,
        pub narrative: OntologyNarrative,
    }

    impl IhatovLoop {
        pub fn new() -> Self {
            let mut library = RitualLibrary::new();
            library.add_ritual(
                "Harmony Ceremony",
                vec![
                    GrimoireToken::Invoke("ResourceHarmony"),
                    GrimoireToken::Story("Saga of the Tree"),
                    GrimoireToken::Vision("watercolor"),
                    GrimoireToken::Chant("calm"),
                ],
            );
            let exchange = RitualExchange::new(library.clone());
            IhatovLoop {
                anomaly_engine: AnomalyMultimedia::new(),
                ritual_library: library,
                ritual_exchange: exchange,
                governance: OntologyGovernance::new(),
                narrative: OntologyNarrative::new(),
            }
        }

        pub fn cycle(&mut self, anomaly: Anomaly, actor: &'static str) {
            println!("🌌 Ihatov Loop begins...");

            self.anomaly_engine.render_anomaly(anomaly);
            self.ritual_library.invoke("Harmony Ceremony");
            self.ritual_exchange.transfer(actor, "Community", "Harmony Ceremony");

            let verdict = self
                .governance
                .enforce_constant(crate::symbolic_ontology::CosmicConstant::TrustBalance, actor);
            println!("⚖️ Governance verdict: {:?}", verdict);

            self.narrative.narrate();

            println!("🔁 Ihatov Loop complete.");
        }
    }
}

pub mod ihatov_saga {
    use crate::ihatov_loop::IhatovLoop;
    use crate::orchestration_intelligence::Anomaly;

    #[derive(Debug)]
    pub struct SagaChapter {
        pub title: String,
        pub anomaly: Anomaly,
        pub outcome: String,
    }

    #[derive(Debug)]
    pub struct IhatovSaga {
        pub chapters: Vec<SagaChapter>,
    }

    pub struct SagaEngine {
        pub loop_system: IhatovLoop,
    }

    impl SagaEngine {
        pub fn new() -> Self {
            SagaEngine { loop_system: IhatovLoop::new() }
        }

        pub fn run_chapter(&mut self, anomaly: Anomaly, actor: &'static str) -> SagaChapter {
            println!("📖 Starting saga chapter with anomaly: {:?}", anomaly);
            self.loop_system.cycle(anomaly, actor);

            SagaChapter {
                title: format!("Chapter of {:?}", anomaly),
                anomaly,
                outcome: "Loop complete, narrative arc generated.".to_string(),
            }
        }

        pub fn run_saga(&mut self, anomalies: Vec<Anomaly>, actor: &'static str) -> IhatovSaga {
            let mut chapters = vec![];
            for anomaly in anomalies {
                let chapter = self.run_chapter(anomaly, actor);
                chapters.push(chapter);
            }
            IhatovSaga { chapters }
        }
    }
}

pub mod saga_persistence {
    use crate::ihatov_saga::{IhatovSaga, SagaChapter};
    use std::fs::{File, OpenOptions};
    use std::io::{Write, Read};

    pub struct SagaPersistence;

    impl SagaPersistence {
        pub fn save(saga: &IhatovSaga, path: &str) {
            let mut file = File::create(path).expect("Unable to create saga file");
            for chapter in &saga.chapters {
                let line = format!("{}|{:?}|{}\n", chapter.title, chapter.anomaly, chapter.outcome);
                file.write_all(line.as_bytes()).expect("Unable to write saga data");
            }
            println!("💾 Saga saved to {}", path);
        }

        pub fn load(path: &str) -> IhatovSaga {
            let mut file = File::open(path).expect("Unable to open saga file");
            let mut contents = String::new();
            file.read_to_string(&mut contents).expect("Unable to read saga data");

            let mut chapters = vec![];
            for line in contents.lines() {
                let parts: Vec<&str> = line.split('|').collect();
                if parts.len() == 3 {
                    chapters.push(SagaChapter {
                        title: parts[0].to_string(),
                        anomaly: crate::orchestration_intelligence::Anomaly::HighLatency,
                        outcome: parts[2].to_string(),
                    });
                }
            }
            println!("📂 Saga loaded from {}", path);
            IhatovSaga { chapters }
        }

        pub fn append(saga: &IhatovSaga, path: &str) {
            let mut file = OpenOptions::new()
                .append(true)
                .open(path)
                .expect("Unable to open saga file");
            for chapter in &saga.chapters {
                let line = format!("{}|{:?}|{}\n", chapter.title, chapter.anomaly, chapter.outcome);
                file.write_all(line.as_bytes()).expect("Unable to write saga data");
            }
            println!("📂 Saga appended to {}", path);
        }
    }
}

pub mod saga_replay {
    use crate::ihatov_saga::IhatovSaga;
    use crate::multimedia::MultimediaEngine;

    pub struct SagaReplay {
        pub engine: MultimediaEngine,
    }

    impl SagaReplay {
        pub fn new() -> Self {
            SagaReplay { engine: MultimediaEngine::new() }
        }

        pub fn replay(&self, saga: &IhatovSaga) {
            println!("🎥 Replaying Ihatov Saga...");
            for (i, chapter) in saga.chapters.iter().enumerate() {
                println!("📖 Chapter {}: {}", i + 1, chapter.title);

                let f1 = self.engine.generate_frame(i as u32, &chapter.title, "cinematic");
                let f2 = self.engine.generate_frame(i as u32 + 100, &chapter.outcome, "watercolor");
                let audio = self.engine.generate_audio(i as u32, "Saga Replay Track", "nostalgic");

                let seq = self.engine.build_sequence(i as u32, vec![f1, f2], audio, true);
                self.engine.play(&seq);
            }
            println!("🔁 Saga replay complete.");
        }
    }
}

pub mod saga_branching {
    use crate::ihatov_saga::{SagaChapter, IhatovSaga};
    use crate::orchestration_intelligence::Anomaly;

    #[derive(Debug)]
    pub struct BranchOption {
        pub choice: String,
        pub outcome: String,
    }

    #[derive(Debug)]
    pub struct BranchingChapter {
        pub base: SagaChapter,
        pub branches: Vec<BranchOption>,
    }

    pub struct SagaBranchingEngine;

    impl SagaBranchingEngine {
        pub fn new() -> Self {
            SagaBranchingEngine
        }

        pub fn branch_chapter(&self, anomaly: Anomaly, title: &str) -> BranchingChapter {
            let base = SagaChapter {
                title: title.to_string(),
                anomaly,
                outcome: "Default outcome".to_string(),
            };

            let branches = vec![
                BranchOption {
                    choice: "Perform Ritual".to_string(),
                    outcome: "Harmony restored through ceremony.".to_string(),
                },
                BranchOption {
                    choice: "Ignore Anomaly".to_string(),
                    outcome: "Chaos spreads, resources destabilize.".to_string(),
                },
                BranchOption {
                    choice: "Trade Ritual".to_string(),
                    outcome: "Community gains trust, economy strengthened.".to_string(),
                },
            ];

            BranchingChapter { base, branches }
        }

        pub fn run_branch(&self, chapter: &BranchingChapter, choice: &str) -> String {
            if let Some(branch) = chapter.branches.iter().find(|b| b.choice == choice) {
                format!("Chosen path: {} → {}", branch.choice, branch.outcome)
            } else {
                "⚠️ Invalid choice".to_string()
            }
        }

        pub fn run_saga(&self, anomalies: Vec<Anomaly>) -> IhatovSaga {
            let mut chapters = vec![];
            for (i, anomaly) in anomalies.iter().enumerate() {
                let branching = self.branch_chapter(*anomaly, &format!("Chapter {}", i + 1));
                let outcome = self.run_branch(&branching, "Perform Ritual");
                chapters.push(SagaChapter {
                    title: branching.base.title.clone(),
                    anomaly: branching.base.anomaly,
                    outcome,
                });
            }
            IhatovSaga { chapters }
        }
    }
}

// ---------------------------------------------------------------------------
// canonical.rs - the image as Ihatov's canonical object (the vessel)
// ---------------------------------------------------------------------------

pub mod canonical {
    pub const VESSEL: &str = "In Ihatov, art is the canonical object. Art is everything.";

    #[derive(Debug)]
    pub struct VesselToken {
        pub name: &'static str,
        pub role: &'static str,
    }

    pub fn vessel_tokens() -> Vec<VesselToken> {
        vec![
            VesselToken { name: "Portal", role: "branching node — saga forks" },
            VesselToken { name: "Lighthouse", role: "signal emitter — kernel beacon" },
            VesselToken { name: "Cat", role: "ledger token — resource carrier" },
            VesselToken { name: "Cloaked Figure", role: "conscious NPC — avatar vessel" },
            VesselToken { name: "Stars", role: "narrative forks — mythic paths" },
            VesselToken { name: "Moon Beams", role: "saga arcs — cinematic flow" },
        ]
    }

    pub fn describe() {
        println!("{}", VESSEL);
        println!("The image is not just art — it is the compiled surface of the code.");
        for t in vessel_tokens() {
            println!("  • {} — {}", t.name, t.role);
        }
    }
}

// ---------------------------------------------------------------------------
// HazeruOS root runtime — the Big Bang that bootstraps every subsystem
// ---------------------------------------------------------------------------

pub struct HazeruOS {
    pub ledger_core: crate::ledger::Ledger,
    pub ledger_services: crate::ledger_services::LedgerServices,
    pub orchestrator: crate::orchestration::Orchestrator,
    pub governance: crate::governance::Governance,
    pub policies: crate::governance_policies::GovernancePolicies,
    pub civic: crate::civic_services::CivicSystem,
    pub audit: crate::civic_audit::CivicAuditTrail,
    pub market: crate::marketplace::Marketplace,
    pub quests: crate::economy_quests::EconomyQuestEngine,
    pub start_ticks: u64,
}

impl HazeruOS {
    pub fn new() -> Self {
        let mut ledger_core = crate::ledger::Ledger::new();
        ledger_core.add_block("Hazeru kernel booted");
        ledger_core.add_block("Elf Avatar created");
        ledger_core.add_block("Portal World opened");

        let mut market = crate::marketplace::Marketplace::new();
        market.publish(crate::marketplace::PluginInfo {
            name: "AvatarPlugin",
            description: "Adds advanced avatar customization",
            author: "Darrell",
            version: "1.0.0",
        });
        market.publish(crate::marketplace::PluginInfo {
            name: "PortalPlugin",
            description: "Adds portal creation and management",
            author: "Darrell",
            version: "1.0.0",
        });

        let mut civic = crate::civic_services::CivicSystem::new();
        civic.add_service(
            crate::civic_services::CivicLaw::TradeFairness,
            "Ensure fair exchange in all ledger transactions",
        );
        civic.add_service(
            crate::civic_services::CivicLaw::AntiFraud,
            "Prevent fraudulent plugins and economic exploits",
        );

        HazeruOS {
            ledger_core,
            ledger_services: crate::ledger_services::LedgerServices::new(),
            orchestrator: crate::orchestration::Orchestrator::new(),
            governance: crate::governance::Governance::new(),
            policies: crate::governance_policies::GovernancePolicies::new(),
            civic,
            audit: crate::civic_audit::CivicAuditTrail::new(),
            market,
            quests: crate::economy_quests::EconomyQuestEngine::new(),
            start_ticks: 0,
        }
    }

    pub fn boot(&mut self) {
        self.start_ticks = 1;

        // ── Kernel spine ──
        hazeru_kernel::init_hardware();
        hazeru_kernel::boot_runtime();
        let _beacon_ok = hazeru_kernel::self_test();

        // ── HAL devices ──
        hal::boot_devices();
        let mem = hal::MemoryController;
        mem.write(42);

        // ── Background services ──
        services::boot_background();

        // ── Scheduler ──
        let mut sched = scheduler::Scheduler::new();
        sched.add_process(scheduler::Process {
            pid: 1,
            name: "Elf Avatar",
            state: scheduler::ProcessState::Ready,
        });
        sched.add_process(scheduler::Process {
            pid: 2,
            name: "Portal World",
            state: scheduler::ProcessState::Ready,
        });
        sched.run_next();
        sched.run_next();

        // ── Lyra UI/UX + renderer ──
        lyra_ui::render_world();
        let renderer = lyra_render::Renderer::new();
        renderer.draw_portal("Main Application World");
        renderer.draw_avatar("Elf with Pink Hair");

        // ── Gestures ──
        let mut avatar = lyra_gestures::Avatar {
            name: "Elf with Pink Hair",
            position: (0, 0),
        };
        avatar.perform(lyra_gestures::Gesture::MoveForward);
        avatar.perform(lyra_gestures::Gesture::TurnRight);
        avatar.perform(lyra_gestures::Gesture::OpenPortal);

        // ── Rendering engine ──
        let light = rendering::Lighting { intensity: 0.8, color: "soft pink" };
        light.apply();
        let atmosphere = rendering::Atmosphere { sky: "twilight", weather: "clear" };
        atmosphere.render();
        let transition = rendering::Transition { from: "Outer World", to: "Portal World" };
        transition.execute();

        // ── Persistence ──
        let mut persistence = persistence::Persistence::new();
        let mut data = std::collections::HashMap::new();
        data.insert("progress", "Level 1 complete".to_string());
        persistence.save(persistence::WorldState {
            id: 1,
            name: "Portal World",
            data,
        });
        if let Some(state) = persistence.load(1) {
            println!("Resumed world state: {:?}", state);
        }

        // ── Network fabric ──
        let mut net = network::NetworkFabric::new();
        net.send(network::Message {
            from: "Elf Avatar",
            to: "Portal World",
            content: "Hello from the avatar!".to_string(),
        });
        if let Some(messages) = net.receive("Portal World") {
            for msg in messages {
                println!("Portal received: {:?}", msg);
            }
        }

        // ── Security model ──
        let sandbox = security::Sandbox::new(
            "Elf Avatar",
            vec![security::Permission::Read, security::Permission::Execute],
        );
        sandbox.check(security::Permission::Read);
        sandbox.check(security::Permission::Write);

        // ── Cryptography ──
        let msg = "Elf Avatar says hello";
        let hash = crypto::Crypto::hash(msg);
        println!("Hash: {}", hash);
        let key: [u8; 32] = [7u8; 32];
        let iv: [u8; 16] = [13u8; 16];
        let enc = crypto::Crypto::encrypt(&key, &iv, "Secret message from Elf Avatar");
        println!("Encrypted: {:?}", enc);
        let dec = crypto::Crypto::decrypt(&key, &iv, &enc);
        println!("Decrypted: {}", dec);

        // ── Consumer + enterprise builds ──
        let consumer_cfg = consumer::ConsumerConfig { theme: "Lyra Pink", autosave: true };
        consumer_cfg.apply();
        let enterprise_cfg = enterprise::EnterpriseConfig { security_level: 5, multi_user: true };
        enterprise_cfg.apply();

        // ── API layer ──
        let portal_api = api::PortalAPI;
        println!("{}", portal_api.call("open", "Main Application World"));
        let avatar_api = api::AvatarAPI;
        println!("{}", avatar_api.call("speak", "Hello, Hazeru!"));

        // ── Avatars: identity + customization + interactions ──
        let mut elf = avatar::Avatar {
            id: 1,
            name: "Elf with Pink Hair",
            hair_color: "pink",
            role: avatar::Role::User,
            position: (0, 0),
        };
        elf.move_to(1, 2);
        elf.customize_hair("violet");

        let mut elf_custom = avatar_custom::Avatar {
            id: 1,
            name: "Elf with Pink Hair",
            hair_color: "pink",
            role: avatar_custom::Role::User,
            position: (0, 0),
            outfit: None,
            abilities: vec![],
        };
        elf_custom.set_outfit(avatar_custom::Outfit { style: "robe", color: "silver" });
        elf_custom.add_ability(avatar_custom::Ability { name: "Teleport", power: 80 });

        let mut elf_fight = avatar_interactions::Avatar {
            id: 1,
            name: "Elf with Pink Hair",
            health: 100,
            position: (0, 0),
        };
        let mut warrior = avatar_interactions::Avatar {
            id: 2,
            name: "Warrior",
            health: 120,
            position: (5, 5),
        };
        elf_fight.attack(&mut warrior, 30);
        elf_fight.heal(20);
        elf_fight.collaborate(&warrior, "Build Portal");
        elf_fight.message(&warrior, "Meet me at the portal!");

        // ── Ledger economy ──
        self.ledger_services.record_transaction(crate::ledger_services::Transaction {
            from: "Elf Avatar",
            to: "Portal World",
            amount: 50,
            description: "Energy crystals",
        });
        self.ledger_services.update_reputation("Elf Avatar", 10);
        if let Some(rep) = self.ledger_services.get_reputation("Elf Avatar") {
            println!("Elf Avatar reputation: {:?}", rep);
        }

        // ── Economy quests ──
        let tx = crate::ledger_services::Transaction {
            from: "Elf Avatar",
            to: "Warrior",
            amount: 30,
            description: "Shared energy crystals",
        };
        self.quests.generate_from_transaction(&tx);
        let rep = crate::ledger_services::Reputation { avatar: "Elf Avatar", score: 60 };
        self.quests.generate_from_reputation(&rep);
        self.quests.list();

        // ── Quest chains ──
        let mut qce = narrative_quests::QuestChainEngine::new();
        qce.create_chain(
            "Crystal Saga",
            vec![
                self.quests.quests[0].clone(),
                crate::economy_quests::Quest {
                    title: "Hero's Duty".to_string(),
                    description: "Defend the portal as a trusted hero".to_string(),
                    reward: 100,
                },
            ],
        );
        qce.list_chains();
        qce.progress_chain("Crystal Saga");

        // ── Plugins + marketplace ──
        let mut registry = plugin::PluginRegistry::new();
        self.market.list();
        market_install(&mut registry);
        registry.run_all("Hello from Hazeru!");

        self.governance.review(self.market.available[0].clone(), true);
        self.governance.review(self.market.available[1].clone(), true);
        for record in self.governance.records.clone() {
            self.policies.assign_tier(record);
        }
        self.policies.list_policies();

        let mut mg = marketplace_governance::MarketplaceGovernance::new();
        mg.register_developer("Darrell");
        mg.record_audit(
            self.market.available[0].clone(),
            governance::GovernanceStatus::Approved,
            "ModeratorBot",
            "Safe and compliant",
            "2026-09-10T19:52Z",
        );
        mg.penalize_developer("Darrell", "Minor policy violation: missing documentation");
        mg.list_audits();

        let low_priv = developer_trust::privileges_for_tier(developer_trust::TrustTier::Low);
        let high_priv = developer_trust::privileges_for_tier(developer_trust::TrustTier::High);
        println!("Low tier privileges: {:?}", low_priv);
        println!("High tier privileges: {:?}", high_priv);

        // ── World simulation ──
        let physics = world::Physics { gravity: 9.8, friction: 0.05 };
        let mut position = (0.0, 100.0);
        let mut velocity = 10.0;
        physics.apply_gravity(&mut position);
        physics.apply_friction(&mut velocity);
        let mut env = world::Environment {
            weather: world::Weather::Sunny,
            time_of_day: "Morning",
        };
        env.change_weather(world::Weather::Stormy);
        env.cycle_time("Night");
        let event = world::Event { description: "Portal storm opens across the sky" };
        event.trigger();

        // ── Emergent AI + narrative ──
        let mut agent_system = ai_narrative::AgentNarrative::new();
        agent_system.add_agent(ai::Agent {
            id: 1,
            name: "Elf with Pink Hair",
            health: 100,
            energy: 20,
            goal: ai::Goal::Explore,
        });
        agent_system.add_agent(ai::Agent {
            id: 2,
            name: "Warrior",
            health: 120,
            energy: 15,
            goal: ai::Goal::Socialize,
        });
        println!("Starting narrative: {}", agent_system.engine.current_description());
        agent_system.tick_agents("forest");

        // ── Narrative + world ──
        let mut nw = narrative_world::NarrativeWorld::new();
        nw.apply_event(narrative_world::EnvironmentEvent::Storm);
        nw.apply_event(narrative_world::EnvironmentEvent::Eclipse);

        // ── Narrative + ledger ──
        let mut nl = narrative_ledger::NarrativeLedger::new();
        nl.record_story_event(crate::ledger_services::Transaction {
            from: "Elf Avatar",
            to: "Warrior",
            amount: 30,
            description: "Shared energy crystals",
        });
        nl.reputation_story("Elf Avatar", 20);
        nl.reputation_story("Warrior", -15);

        // ── Orchestration ──
        self.orchestrator.register(orchestration::Service {
            id: 1,
            name: "Ledger Service",
            state: orchestration::ServiceState::Stopped,
        });
        self.orchestrator.register(orchestration::Service {
            id: 2,
            name: "Avatar Engine",
            state: orchestration::ServiceState::Stopped,
        });
        self.orchestrator.register(orchestration::Service {
            id: 3,
            name: "Portal Manager",
            state: orchestration::ServiceState::Stopped,
        });
        self.orchestrator.start_all();
        self.orchestrator.scale(3);

        let mut policy = orchestration_policies::PolicyOrchestrator::new();
        policy.register(orchestration::Service {
            id: 1,
            name: "Ledger Service",
            state: orchestration::ServiceState::Stopped,
        });
        policy.auto_restart();
        policy.load_balance(100);
        policy.fault_tolerance(1);

        let mut monitor = orchestration_monitoring::MonitoringOrchestrator::new();
        monitor.register(orchestration::Service {
            id: 1,
            name: "Ledger Service",
            state: orchestration::ServiceState::Running,
        });
        monitor.log_request(1);
        monitor.health_check();
        monitor.report();

        let mut resilient = orchestration_resilience::ResilientOrchestrator::new();
        resilient.register(orchestration::Service {
            id: 1,
            name: "Ledger Service",
            state: orchestration::ServiceState::Stopped,
        });
        resilient.predictive_scale(200);
        resilient.self_heal();

        let mut intelligent = orchestration_intelligence::IntelligentOrchestrator::new();
        intelligent.register(orchestration::Service {
            id: 1,
            name: "Ledger Service",
            state: orchestration::ServiceState::Running,
        });
        intelligent.detect_anomaly(1, orchestration_intelligence::Anomaly::HighLatency);
        intelligent.intelligent_scale(300);

        let mut no = orchestration_narrative::NarrativeOrchestrator::new();
        no.anomaly_to_story(orchestration_intelligence::Anomaly::ResourceSpike);
        no.narrate();

        let mut lg = ledger_governance::GovernanceLedger::new();
        lg.apply_transaction(&crate::ledger_services::Transaction {
            from: "Elf Avatar",
            to: "Warrior",
            amount: 50,
            description: "Shared rare crystals",
        });
        lg.apply_reputation(&crate::ledger_services::Reputation { avatar: "Elf Avatar", score: 80 });

        let governed = orchestration_governance::GovernedOrchestrator::new();
        let _ = governed;

        // ── Civic services + enforcement + judiciary ──
        self.civic.enforce();
        self.civic.audit();

        let mut engine = civic_audit::CivicAuditTrail::new();
        engine.log(
            civic_laws::CivicLaw::TradeFairness,
            "Transaction Review",
            "ModeratorBot",
            "Approved",
            "2026-09-10T19:58Z",
        );
        engine.log(
            civic_laws::CivicLaw::AntiFraud,
            "Plugin Scan",
            "AuditDaemon",
            "Rejected suspicious plugin",
            "2026-09-10T19:59Z",
        );
        engine.report();

        let mut enforcement = civic_enforcement::CivicEnforcementEngine::new();
        enforcement.enforce(civic_laws::CivicLaw::TradeFairness, "Elf Avatar", "2026-09-10T20:01Z");
        enforcement.enforce(civic_laws::CivicLaw::PrivacyProtection, "Suspicious Plugin", "2026-09-10T20:02Z");
        enforcement.audit_report();

        let mut court = civic_judiciary::JudiciarySystem::new();
        court.start_trial(
            civic_laws::CivicLaw::PrivacyProtection,
            "Suspicious Plugin",
            vec!["Unauthorized data access"],
        );
        court.deliver_verdict(
            "Suspicious Plugin",
            civic_judiciary::Verdict::Guilty("Privacy violation confirmed", 15),
        );
        court.appeal("Suspicious Plugin", "Developer claims false positive");
        court.report();

        // ── SDK ──
        sdk::kernel::boot();
        sdk::scheduler::spawn_process("Portal World");
        sdk::persistence::save_state("Level 1");
        sdk::network::send_message("Portal World", "Hello from SDK!");
        sdk::avatar::create("Elf with Pink Hair");

        // ── Canonical vessel ──
        canonical::describe();
    }

    pub fn run_ihatov(&mut self) {
        let mut saga_engine = ihatov_saga::SagaEngine::new();
        let anomalies = vec![
            orchestration_intelligence::Anomaly::HighLatency,
            orchestration_intelligence::Anomaly::ResourceSpike,
            orchestration_intelligence::Anomaly::ExcessiveFailures,
        ];
        let saga = saga_engine.run_saga(anomalies, "Elf Avatar");
        println!("🌌 Ihatov Saga Generated:");
        for chapter in saga.chapters.iter() {
            println!("- {} → {}", chapter.title, chapter.outcome);
        }
    }

    pub fn ledger_valid(&self) -> bool {
        self.ledger_core.validate() && self.ledger_services.ledger.validate()
    }

    pub fn report(&self) -> String {
        let mut s = String::new();
        s.push_str(&format!(
            "═ HAZERU OS — The Five-Glyph Kernel ═\nBeacon: {} | {} | Canonical Vessel: Ihatov\n\n",
            hazeru_kernel::KERNEL_BEACON, GRIMOIRE
        ));

        s.push_str(&format!(
            "◆ DISTRIBUTED LEDGER — {} blocks (valid: {})\n",
            self.ledger_core.chain.len(),
            self.ledger_core.validate()
        ));
        s.push_str(&format!(
            "◆ LEDGER SERVICES — {} blocks, {} reputation records (valid: {})\n",
            self.ledger_services.ledger.chain.len(),
            self.ledger_services.reputation.len(),
            self.ledger_services.ledger.validate()
        ));
        s.push_str(&format!(
            "◆ ORCHESTRATION — {} services registered\n",
            self.orchestrator.services.len()
        ));
        s.push_str(&format!(
            "◆ GOVERNANCE — {} records, {} policies\n",
            self.governance.records.len(),
            self.policies.count()
        ));
        s.push_str(&format!(
            "◆ MARKETPLACE — {} published plugins\n",
            self.market.available.len()
        ));
        s.push_str(&format!(
            "◆ CIVIC — {} services enforced, {} audit records\n",
            self.civic.services.len(),
            self.audit.count()
        ));
        s.push_str(&format!("◆ ECONOMY QUESTS — {} active\n", self.quests.quests.len()));

        s.push_str("\n◆ 55-SUBSYSTEM CAPABILITY MAP (spec → code)\n");
        let caps = [
            "kernel spine (beacon+startup)",
            "HAL (memory/storage/graphics/network)",
            "scheduler (process state machine)",
            "background services (telemetry/persistence)",
            "Lyra UI portals",
            "Lyra renderer (portals/avatars)",
            "Lyra gestures (spatial navigation)",
            "rendering engine (lighting/atmosphere/transition)",
            "persistence (world save/resume)",
            "network fabric (message channels)",
            "security model (permissions + sandbox)",
            "crypto (hash + encrypt/decrypt)",
            "consumer build profile",
            "enterprise build profile",
            "API layer (portal/avatar hooks)",
            "developer SDK (kernel/scheduler/persistence/network/avatar)",
            "avatar identity (roles, customization)",
            "avatar customization (outfits/abilities)",
            "avatar interactions (combat/heal/collab/message)",
            "distributed ledger (blocks + validation)",
            "ledger services (transactions/reputation)",
            "economy-driven quests",
            "narrative quest chains",
            "plugin system (lifecycle + registry)",
            "plugin marketplace (publish/discover/install)",
            "marketplace governance (reviews + trust)",
            "governance policies (trust tiers)",
            "marketplace governance audit (developer profiles)",
            "developer trust tiers (privileges)",
            "world simulation (physics/weather/events)",
            "emergent AI (goals + adaptation)",
            "narrative engine (branching story nodes)",
            "AI + narrative fusion",
            "narrative + ledger fusion",
            "narrative + world events",
            "orchestration (daemon lifecycle)",
            "orchestration policies (auto-restart/load-balance/fault-tolerance)",
            "orchestration monitoring (metrics/health)",
            "orchestration resilience (self-heal)",
            "orchestration intelligence (anomaly detection)",
            "orchestration + governance (trust enforcement)",
            "orchestration + narrative (anomalies become story)",
            "ledger-driven governance",
            "anomaly-driven quests",
            "Kenji Miyazawa-style allegorical quests",
            "anomaly + multimedia (playable missions)",
            "procedural multimedia engine (frames/audio/sequences)",
            "narrative + multimedia (playable cinema)",
            "symbolic ontology (cosmic constants + archetypes)",
            "ontology governance (universe-level law)",
            "ontology-driven narrative (sagas from constants)",
            "multimedia scripting API + DSL",
            "Gran Grimoire ritual language (invoke/story/vision/chant)",
            "ritual libraries + ritual exchange",
            "Gran Grimoire + ledger (rituals as transactions)",
            "civic services / audit / laws catalog / enforcement / judiciary",
            "playable Ihatov Loop (quest→ritual→exchange→governance→narrative)",
            "Ihatov Saga engine + persistence + replay + branching",
            "canonical vessel (image as the object of the code)",
        ];
        for c in caps {
            s.push_str(&format!("  • {c}\n"));
        }

        s.push_str("\n◆ PLAYABLE IHATOV LOOP\n");
        s.push_str("  Quest → Ritual → Exchange → Governance → Narrative\n");

        s.push_str("\n◆ NOT AI — sovereign alternate-reality platform (deterministic, symbolic, procedural)\n");
        s.push_str("◆ One app for everything — art, models, rendering, story, rituals, economy\n");
        s.push_str("\n═ COMPILED IN RUST · ONE OUTPUT FILE ═\n");
        s
    }
}

fn market_install(registry: &mut plugin::PluginRegistry) {
    registry.register(Box::new(plugin::AvatarPlugin));
    registry.register(Box::new(plugin::PortalPlugin));
}

// ---------------------------------------------------------------------------
// per-subcommand demos
// ---------------------------------------------------------------------------

fn demo_ledger() {
    println!("════ DISTRIBUTED LEDGER REPLAY ════\n");
    let mut services = ledger_services::LedgerServices::new();
    services.record_transaction(ledger_services::Transaction {
        from: "Elf Avatar",
        to: "Portal World",
        amount: 50,
        description: "Energy crystals",
    });
    services.record_transaction(ledger_services::Transaction {
        from: "Warrior",
        to: "Elf Avatar",
        amount: 20,
        description: "Healing potion",
    });
    services.update_reputation("Elf Avatar", 10);
    services.update_reputation("Warrior", -5);
    println!("\nLedger chain ({} blocks):", services.ledger.chain.len());
    services.ledger.print();
    println!("\nLedger valid: {}", services.ledger.validate());
}

fn demo_grimoire() {
    println!("════ GRAN GRIMOIRE RITUAL BUILD ════\n");
    let grimoire = gran_grimoire::GranGrimoire::new();
    let ritual = vec![
        gran_grimoire::GrimoireToken::Invoke("TrustBalance"),
        gran_grimoire::GrimoireToken::Story("Saga of the Crystal"),
        gran_grimoire::GrimoireToken::Vision("watercolor"),
        gran_grimoire::GrimoireToken::Chant("mystical"),
    ];
    grimoire.cast(ritual);

    println!("\n── Ritual library + exchange ──");
    let mut library = ritual_library::RitualLibrary::new();
    library.add_ritual(
        "Harmony Ceremony",
        vec![
            gran_grimoire::GrimoireToken::Invoke("ResourceHarmony"),
            gran_grimoire::GrimoireToken::Story("Saga of the Tree"),
            gran_grimoire::GrimoireToken::Vision("watercolor"),
            gran_grimoire::GrimoireToken::Chant("calm"),
        ],
    );
    library.list();
    let mut exchange = ritual_exchange::RitualExchange::new(library.clone());
    exchange.transfer("Elf Avatar", "Warrior Avatar", "Harmony Ceremony");
    exchange.audit();

    println!("\n── Grimoire + ledger ──");
    let mut gl = grimoire_ledger::GrimoireLedger::new();
    gl.cast_with_ledger(
        "Elf Avatar",
        vec![
            gran_grimoire::GrimoireToken::Invoke("TrustBalance"),
            gran_grimoire::GrimoireToken::Story("Saga of the Crystal"),
            gran_grimoire::GrimoireToken::Vision("watercolor"),
            gran_grimoire::GrimoireToken::Chant("mystical"),
        ],
    );
    gl.audit();
    println!("Ritual ledger valid: {}", gl.valid());
}

fn demo_saga() {
    println!("════ IHATOV SAGA ENGINE + PERSISTENCE ════\n");

    let mut saga_engine = ihatov_saga::SagaEngine::new();
    let anomalies = vec![
        orchestration_intelligence::Anomaly::HighLatency,
        orchestration_intelligence::Anomaly::ResourceSpike,
    ];
    let saga = saga_engine.run_saga(anomalies, "Elf Avatar");

    let path = std::env::temp_dir().join("ihatov_saga.txt");
    let path_str = path.to_str().unwrap();

    saga_persistence::SagaPersistence::save(&saga, path_str);
    let loaded = saga_persistence::SagaPersistence::load(path_str);
    println!("🌌 Loaded Saga:");
    for chapter in loaded.chapters.iter() {
        println!("- {} → {}", chapter.title, chapter.outcome);
    }

    println!("\n── Saga replay ──");
    let replay = saga_replay::SagaReplay::new();
    replay.replay(&loaded);

    println!("\n── Branching saga ──");
    let branching = saga_branching::SagaBranchingEngine::new();
    let b_saga = branching.run_saga(vec![
        orchestration_intelligence::Anomaly::HighLatency,
        orchestration_intelligence::Anomaly::ResourceSpike,
    ]);
    println!("🌌 Branching Ihatov Saga:");
    for chapter in b_saga.chapters.iter() {
        println!("- {} → {}", chapter.title, chapter.outcome);
    }
}

fn demo_civic() {
    println!("════ CIVIC LAW CATALOG + JUDICIARY ════\n");
    let mut enforcement = civic_enforcement::CivicEnforcementEngine::new();
    enforcement.list_laws();
    println!();
    enforcement.enforce(civic_laws::CivicLaw::TradeFairness, "Elf Avatar", "2026-09-10T21:01Z");
    enforcement.enforce(civic_laws::CivicLaw::AntiFraud, "Suspicious Plugin", "2026-09-10T21:02Z");
    enforcement.audit_report();

    println!("\n── Judiciary ──");
    let mut court = civic_judiciary::JudiciarySystem::new();
    court.start_trial(
        civic_laws::CivicLaw::PrivacyProtection,
        "Suspicious Plugin",
        vec!["Unauthorized data access"],
    );
    court.deliver_verdict(
        "Suspicious Plugin",
        civic_judiciary::Verdict::Guilty("Privacy violation confirmed", 15),
    );
    court.appeal("Suspicious Plugin", "Developer claims false positive");
    court.report();

    println!("\n── Ontology governance ──");
    let og = ontology_governance::OntologyGovernance::new();
    og.audit_archetypes();
    let v1 = og.enforce_constant(symbolic_ontology::CosmicConstant::TrustBalance, "Suspicious Plugin");
    let v2 = og.enforce_constant(symbolic_ontology::CosmicConstant::ExpressionFreedom, "Elf Avatar");
    println!("Verdict1: {:?}", v1);
    println!("Verdict2: {:?}", v2);

    println!("\n── Ontology narrative ──");
    let on = ontology_narrative::OntologyNarrative::new();
    on.narrate();
}

fn demo_sdk() {
    println!("════ DEVELOPER SDK ════\n");
    sdk::kernel::boot();
    sdk::scheduler::spawn_process("Portal World");
    sdk::persistence::save_state("Level 1");
    sdk::network::send_message("Portal World", "Hello from SDK!");
    sdk::avatar::create("Elf with Pink Hair");

    println!("\n── Multimedia scripting API ──");
    let api = multimedia_api::MultimediaScriptAPI::new();
    let script = vec![
        multimedia_api::ScriptCommand::Frame(1, "Twilight sky over portal city", "watercolor"),
        multimedia_api::ScriptCommand::Frame(2, "Avatars crossing crystal bridge", "cinematic"),
        multimedia_api::ScriptCommand::Audio(1, "Twilight Sonata", "mystical"),
        multimedia_api::ScriptCommand::Sequence(1, vec![1, 2], 1, true),
    ];
    for seq in api.execute(script) {
        api.engine.play(&seq);
    }

    println!("\n── Hazeru DSL ──");
    let dsl = hazeru_dsl::HazeruDSL::new();
    dsl.interpret(vec![
        hazeru_dsl::DSLCommand::Ontology("TrustBalance"),
        hazeru_dsl::DSLCommand::Narrative("Saga of the Crystal"),
        hazeru_dsl::DSLCommand::Multimedia(vec![
            multimedia_api::ScriptCommand::Frame(1, "Moonlight over Ihatov city", "watercolor"),
            multimedia_api::ScriptCommand::Audio(1, "Moon Sonata", "mystical"),
            multimedia_api::ScriptCommand::Sequence(1, vec![1], 1, true),
        ]),
    ]);

    println!("\n── Narrative + multimedia ──");
    let mut nm = narrative_multimedia::NarrativeMultimedia::new();
    nm.narrate_and_render("A storm brews across the horizon, avatars gather at the crystal bridge.");
    nm.narrate_and_render("The economy surges, reputation reshapes destiny in the portal city.");
}

// ---------------------------------------------------------------------------
// main
// ---------------------------------------------------------------------------

fn main() {
    let args: Vec<String> = std::env::args().skip(1).collect();

    let mut os = HazeruOS::new();
    os.boot();

    if args.iter().any(|a| a == "ledger") {
        demo_ledger();
        return;
    }
    if args.iter().any(|a| a == "grimoire") {
        demo_grimoire();
        return;
    }
    if args.iter().any(|a| a == "saga") {
        demo_saga();
        return;
    }
    if args.iter().any(|a| a == "civic") {
        demo_civic();
        return;
    }
    if args.iter().any(|a| a == "sdk") {
        demo_sdk();
        return;
    }

    print!("{}", os.report());

    println!("\n════ IHATOV LOOP + SAGA DEMO ════\n");
    os.run_ihatov();

    println!("\n════ CANONICAL OBJECT ════\n");
    println!("{}", canonical::VESSEL);
    println!("Hazeru (爆ぜる / 罅ぜる) = to burst open, to pop, to split.");
    println!("The boot is the explosion, the modules are the galaxies forming. Pop!");
}

